<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Annu AI</title>

<style>
*{box-sizing:border-box}

body{
 margin:0;
 background:#0b1020;
 color:#fff;
 font-family:Arial,sans-serif;
}

.app{
 max-width:700px;
 margin:auto;
 height:100vh;
 display:flex;
 flex-direction:column;
}

header{
 padding:18px;
 text-align:center;
 background:#111827;
 border-bottom:1px solid #263044;
}

.logo{
 font-size:25px;
 font-weight:bold;
}

.status{
 color:#22c55e;
 font-size:12px;
 margin-top:5px;
}

#chat{
 flex:1;
 overflow-y:auto;
 padding:18px;
}

.welcome{
 text-align:center;
 margin-top:25%;
}

.welcome h1{
 font-size:34px;
}

.welcome p{
 color:#aeb8ca;
}

.msg{
 padding:13px 16px;
 margin:12px 0;
 max-width:85%;
 border-radius:18px;
 line-height:1.5;
 white-space:pre-wrap;
}

.user{
 background:#2563eb;
 margin-left:auto;
 border-bottom-right-radius:5px;
}

.ai{
 background:#1f2937;
 margin-right:auto;
 border-bottom-left-radius:5px;
}

.bottom{
 padding:12px;
 background:#111827;
 border-top:1px solid #263044;
 display:flex;
 gap:8px;
}

input{
 flex:1;
 border:0;
 outline:0;
 padding:15px;
 border-radius:25px;
 background:#202938;
 color:white;
 font-size:16px;
}

button{
 width:50px;
 height:50px;
 border:0;
 border-radius:50%;
 background:#2563eb;
 color:white;
 font-size:21px;
}

button:active{
 transform:scale(.94);
}
</style>
</head>

<body>

<div class="app">

<header>
 <div class="logo">🤖 Annu AI</div>
 <div class="status">● Online</div>
</header>

<div id="chat">

<div class="welcome" id="welcome">
 <h1>Namaste 👋</h1>
 <p>Main Annu AI hoon</p>
 <p>Aap mujhse kuch bhi pooch sakte ho.</p>
</div>

</div>

<div class="bottom">

<button onclick="voice()">🎤</button>

<input
 id="input"
 placeholder="Annu AI se poochho..."
 onkeydown="if(event.key==='Enter')send()">

<button onclick="send()">➤</button>

</div>

</div>

<script>

const input=document.getElementById("input");
const chat=document.getElementById("chat");
const welcome=document.getElementById("welcome");

function add(text,type){

 let div=document.createElement("div");

 div.className="msg "+type;
 div.innerText=text;

 chat.appendChild(div);
 chat.scrollTop=chat.scrollHeight;
}

function send(){

 let text=input.value.trim();

 if(!text)return;

 welcome.style.display="none";

 add(text,"user");

 input.value="";

 setTimeout(()=>{

   let answer=ai(text);

   add(answer,"ai");

   speak(answer);

 },600);
}


function ai(text){

 let t=text.toLowerCase();

 if(t.includes("hello") ||
    t.includes("hi") ||
    t.includes("namaste")){

   return "Namaste 👋 Main Annu AI hoon. Aapki help karne ke liye ready hoon.";
 }

 if(t.includes("naam")){

   return "Mera naam Annu AI hai 🤖";
 }

 if(t.includes("kaise ho")){

   return "Main bilkul theek hoon 😊 Aap batao, main aapki kya help karun?";
 }

 if(t.includes("time")){

   return "Abhi time hai: "+
   new Date().toLocaleTimeString("hi-IN");
 }

 if(t.includes("date")){

   return "Aaj ki date hai: "+
   new Date().toLocaleDateString("hi-IN");
 }

 return "Aapne kaha: \""+text+"\"\n\n"+
        "Main Annu AI hoon 🤖\n"+
        "Real AI model connect karne ke baad main iska advanced answer de sakungi.";
}


// 🎤 Voice input

function voice(){

 const SpeechRecognition=
 window.SpeechRecognition ||
 window.webkitSpeechRecognition;

 if(!SpeechRecognition){

   alert("Voice feature is browser mein supported nahi hai.");
   return;
 }

 const r=new SpeechRecognition();

 r.lang="hi-IN";

 r.start();

 r.onresult=function(e){

   input.value=e.results[0][0].transcript;

   send();

 };

}


// 🔊 Voice reply

function speak(text){

 if(!window.speechSynthesis)return;

 let s=new SpeechSynthesisUtterance(text);

 s.lang="hi-IN";
 s.rate=.9;

 speechSynthesis.cancel();
 speechSynthesis.speak(s);
}

</script>

</body>
</html>    
        
