let btn=document.querySelector("#btn")
let content=document.querySelector("#content")





function speak(text){

let text_speak = new SpeechSynthesisUtterance(text)

window.speechSynthesis.onvoiceschanged = () => {

let voices = window.speechSynthesis.getVoices()


let femaleVoice = voices.find(voice => 
    voice.name.toLowerCase().includes("female") ||
    voice.name.toLowerCase().includes("zira") ||
    voice.name.toLowerCase().includes("susan")
)

text_speak.voice = femaleVoice || voices[1]

text_speak.rate = 0.7
text_speak.pitch = 1.5
text_speak.volume = 1
text_speak.lang = "hi-IN"

window.speechSynthesis.speak(text_speak)

}

}


function wishMe(){
    let day=new Date()
    let hours=day.getHours()
    if(hours>=0 && hours<12){
        speak("good morning")
    }
    else if(hours>=12 && hours<16){
        speak("good afternoon sir")

    }
    else{
        speak("good evening sir")
        
    }
}
window.addEventListener('load',()=>{
    wishMe()
})


window.addEventListener("load", () => {

let SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition

let recognition = new SpeechRecognition() 


recognition.onresult = (event) => {

let transcript = event.results[0][0].transcript

content.innerText = transcript

takeCommand(transcript.toLowerCase())

}

btn.addEventListener("click", () => {
recognition.start()   

})

function takeCommand(message){ 

if(message.includes("hello")){
speak("Hello sir, what can I help you")
}
else if(message.includes("who are you")){  
    speak("i am shifraa,created by abhishek")
}
else if(message.includes("youtube")){
    speak("opening youtube")
    window.open("https://www.youtube.com")
    
}
else if(message.includes("google")){
    speak("opening google")
    window.open("https://www.google.com/")
    
}
else if(message.includes("time")){
let time=new Date().toLocaleString(undefined,{hour:"numeric",minute:"numeric"})
speak(time)
}

else if(message.includes("whatsapp")){
    speak("opening whatsapp")
    window.open("whatsapp://")
}

else{
speak(`i found in internet about ${message}`)
window.open(`https://www.google.com/search?q=${message}`)
}

}
})

