<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MUNA BARAKATI | Smart Login</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}

body{
  min-height:100vh;
  background:radial-gradient(circle at top,#00f5ff,#020024);
  display:flex;
  align-items:center;
  justify-content:center;
  overflow:hidden;
  color:#fff;
}

/* PARTICLES */
.particle{
  position:absolute;
  width:6px;height:6px;
  background:#00f5ff;
  border-radius:50%;
  opacity:.6;
  animation:float 8s linear infinite;
}
@keyframes float{
  from{transform:translateY(100vh)}
  to{transform:translateY(-10vh)}
}

/* CARD */
.card{
  width:100%;
  max-width:380px;
  padding:35px;
  border-radius:20px;
  background:rgba(255,255,255,.12);
  backdrop-filter:blur(16px);
  border:1px solid rgba(255,255,255,.3);
  box-shadow:0 0 40px rgba(0,245,255,.6);
  z-index:10;
  animation:zoom .8s ease;
}
@keyframes zoom{
  from{opacity:0;transform:scale(.8)}
  to{opacity:1;transform:scale(1)}
}

.logo{
  text-align:center;
  font-size:26px;
  font-weight:700;
  letter-spacing:2px;
  color:#00f5ff;
}
.subtitle{
  text-align:center;
  font-size:14px;
  opacity:.85;
  margin:10px 0 25px;
}

input{
  width:100%;
  padding:14px;
  border-radius:12px;
  border:none;
  margin-bottom:15px;
  background:rgba(255,255,255,.18);
  color:#fff;
}
input::placeholder{color:#ddd}
input:focus{outline:none;box-shadow:0 0 10px #00f5ff}

button{
  width:100%;
  padding:14px;
  border:none;
  border-radius:12px;
  background:linear-gradient(90deg,#00f5ff,#0066ff);
  color:#000;
  font-weight:700;
  cursor:pointer;
  box-shadow:0 0 15px #00f5ff;
  transition:.3s;
}
button:hover{transform:scale(1.05)}

.menu{display:none}
.menu h3{
  text-align:center;
  color:#00f5ff;
  margin-bottom:20px;
}
.link{
  display:block;
  text-decoration:none;
  padding:14px;
  border-radius:12px;
  margin-bottom:12px;
  background:rgba(255,255,255,.18);
  color:#fff;
  text-align:center;
  font-weight:600;
  transition:.3s;
}
.link:hover{background:#00f5ff;color:#000}

.logout{
  background:#ff004c;
  color:#fff;
  box-shadow:0 0 15px #ff004c;
}
</style>
</head>
<body>

<!-- AUDIO -->
<audio id="bgm" loop>
  <source src="https://assets.mixkit.co/music/preview/mixkit-tech-house-vibes-130.mp3">
</audio>

<audio id="click">
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-modern-click-box-check-1120.mp3">
</audio>

<audio id="success">
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-futuristic-confirmation-268.mp3">
</audio>

<script>
/* PARTICLES */
for(let i=0;i<35;i++){
  let p=document.createElement("div");
  p.className="particle";
  p.style.left=Math.random()*100+"vw";
  p.style.animationDuration=5+Math.random()*8+"s";
  document.body.appendChild(p);
}
</script>

<div class="card">

<!-- LOGIN -->
<div id="loginBox">
  <div class="logo">MUNA BARAKATI</div>
  <div class="subtitle">AI Secure Technology Access</div>

  <input id="user" placeholder="Username">
  <input id="pass" type="password" placeholder="Password">
  <button onclick="login()">LOGIN SYSTEM</button>
</div>

<!-- MENU -->
<div class="menu" id="menuBox">
  <h3>CONTROL PANEL</h3>

  <a class="link" href="https://google.com" target="_blank">🌐 Google</a>
  <a class="link" href="https://youtube.com" target="_blank">▶ YouTube</a>
  <a class="link" href="https://droid10.my.id" target="_blank">📱 LPP & VARIANCE</a>

  <button class="logout" onclick="logout()">LOGOUT</button>
</div>

</div>

<script>
const click=document.getElementById("click");
const success=document.getElementById("success");
const bgm=document.getElementById("bgm");

/* VOICE AI */
function speak(text){
  let msg=new SpeechSynthesisUtterance(text);
  msg.lang="id-ID";
  msg.rate=0.95;
  msg.pitch=1;
  speechSynthesis.speak(msg);
}

function login(){
  click.play();
  bgm.play(); // mulai musik setelah interaksi
  if(user.value==="admin" && pass.value==="12345"){
    setTimeout(()=>{
      success.play();
      speak("Login berhasil. Selamat datang di sistem Muna Barakati.");
      loginBox.style.display="none";
      menuBox.style.display="block";
    },400);
  }else{
    speak("Akses ditolak. Username atau password salah.");
    alert("ACCESS DENIED");
  }
}

function logout(){
  click.play();
  speak("Anda telah keluar dari sistem.");
  menuBox.style.display="none";
  loginBox.style.display="block";
}
</script>

</body>
</html>
