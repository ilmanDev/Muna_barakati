<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MUNA BARAKATI</title>

<style>
:root{
  --bg:#eef5ff;
  --card:#ffffff;
  --text:#0b1c2d;
  --primary:#0a66ff;
  --accent:#00d4ff;
}
body.dark{
  --bg:#020c1b;
  --card:#071a33;
  --text:#eaf2ff;
  --primary:#3b8cff;
  --accent:#00e0ff;
}

*{box-sizing:border-box;font-family:system-ui,-apple-system}
body{
  margin:0;min-height:100vh;
  background:var(--bg);
  display:flex;justify-content:center;align-items:center;
  color:var(--text);
  transition:.4s;
}

/* SPLASH */
#splash{
  position:fixed;inset:0;
  background:linear-gradient(135deg,var(--primary),var(--accent));
  display:flex;flex-direction:column;
  justify-content:center;align-items:center;
  color:#fff;z-index:999;
}
.loader{
  width:42px;height:42px;
  border:3px solid rgba(255,255,255,.3);
  border-top:3px solid #fff;
  border-radius:50%;
  margin-top:18px;
  animation:spin 1s linear infinite;
}
@keyframes spin{to{transform:rotate(360deg);}}

/* CARD */
.card{
  background:var(--card);
  width:100%;max-width:420px;
  padding:26px;border-radius:26px;
  box-shadow:0 30px 70px rgba(0,0,0,.2);
  display:none;
  transition:.4s;
}

/* TOGGLE */
.toggle{
  position:absolute;
  top:16px;right:16px;
  width:42px;height:42px;
  border-radius:50%;
  background:linear-gradient(135deg,var(--primary),var(--accent));
  color:#fff;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;
  font-size:20px;
  box-shadow:0 10px 25px rgba(0,0,0,.25);
}

/* LOGO */
.logo{
  text-align:center;
  font-size:28px;
  font-weight:900;
  background:linear-gradient(90deg,var(--primary),var(--accent));
  -webkit-background-clip:text;
  color:transparent;
}
.subtitle{text-align:center;color:#6b7c93;margin-bottom:12px}

/* FACE */
.face-wrap{position:relative}
video{
  width:100%;
  border-radius:20px;
  background:#000;
}
.scan-line{
  position:absolute;left:0;right:0;height:3px;
  background:linear-gradient(90deg,transparent,var(--accent),transparent);
  animation:scan 2s linear infinite;
}
@keyframes scan{0%{top:0}100%{top:100%}}
.face-frame{
  position:absolute;inset:12px;
  border:2px solid var(--accent);
  border-radius:18px;
}
.scan-text{text-align:center;margin:10px 0;font-weight:700}

.btn{
  width:100%;
  padding:14px;border:none;
  border-radius:18px;
  background:linear-gradient(135deg,var(--primary),var(--accent));
  color:#fff;font-size:16px;font-weight:800;
  cursor:pointer;
}

/* MENU */
.menu{display:none}
.menu h3{text-align:center;margin-bottom:16px}
.grid{
  display:grid;grid-template-columns:repeat(2,1fr);gap:16px
}
.item{
  background:linear-gradient(180deg,var(--card),#eaf2ff);
  border-radius:20px;
  padding:18px;
  text-align:center;
  text-decoration:none;
  color:var(--text);
  font-weight:800;
  box-shadow:0 12px 30px rgba(0,0,0,.15);
  transition:.3s;
}
body.dark .item{
  background:linear-gradient(180deg,#0a254f,#071a33);
}
.item:hover{transform:translateY(-6px)}
.icon svg{width:34px;height:34px;fill:var(--primary);margin-bottom:6px}

.logout{
  margin-top:20px;
  background:#ff4d4d;color:#fff;
  padding:14px;border-radius:16px;
  text-align:center;font-weight:800;
  cursor:pointer;
}
</style>
</head>

<body>

<!-- SPLASH -->
<div id="splash">
  <h1>MUNA BARAKATI</h1>
  <p>Smart Secure App</p>
  <div class="loader"></div>
</div>

<div class="card" id="app">
<div class="toggle" onclick="toggleMode()">🌙</div>

<!-- LOGIN -->
<div id="loginBox">
  <div class="logo">MUNA BARAKATI</div>
  <div class="subtitle">Face ID Verification</div>

  <div class="face-wrap">
    <video id="video" autoplay muted></video>
    <div class="scan-line"></div>
    <div class="face-frame"></div>
  </div>

  <div class="scan-text" id="scanText">Arahkan wajah ke kamera</div>
  <button class="btn" onclick="startScan()">SCAN WAJAH</button>
</div>

<!-- MENU -->
<div id="menuBox" class="menu">
  <h3>Menu Utama</h3>

  <div class="grid">
    <a href="https://droid10.my.id/" target="_blank" class="item">
      <div class="icon"><svg viewBox="0 0 24 24"><path d="M3 9l1-5h16l1 5H3z"/></svg></div>
      Toko
    </a>
    <a href="https://ilmandev.github.io/portoilman/" target="_blank" class="item">
      <div class="icon"><svg viewBox="0 0 24 24"><path d="M10 15l5-3-5-3v6z"/></svg></div>
      Portofolio
    </a>
    <a href="https://wa.me/6287872921421" target="_blank" class="item">
      <div class="icon"><svg viewBox="0 0 24 24"><path d="M12 2a10 10 0 0 0-8.9 14.5"/></svg></div>
      WhatsApp
    </a>
    <a href="https://maps.google.com" target="_blank" class="item">
      <div class="icon"><svg viewBox="0 0 24 24"><path d="M12 2c-4 0-7 3-7 7"/></svg></div>
      Maps
    </a>
  </div>

  <div class="logout" onclick="logout()">Logout</div>
</div>
</div>

<!-- SOUND -->
<audio id="clickSound" preload="auto">
  <source src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3">
</audio>

<audio id="scanSound" preload="auto">
  <source src="https://assets.mixkit.co/active_storage/sfx/2453/2453-preview.mp3">
</audio>

<script>
let stream;
const clickSound=document.getElementById("clickSound");
const scanSound=document.getElementById("scanSound");

/* MODE */
function toggleMode(){
  document.body.classList.toggle("dark");
}

/* SPLASH */
setTimeout(()=>{
  splash.style.display="none";
  app.style.display="block";
},1500);

/* CLICK SOUND */
document.addEventListener("click",e=>{
  const t=e.target.closest("button,.item,.logout,.toggle");
  if(!t) return;
  clickSound.currentTime=0;
  clickSound.play().catch(()=>{});
});

/* CAMERA */
async function startCamera(){
  stream=await navigator.mediaDevices.getUserMedia({video:true});
  video.srcObject=stream;
}

/* FACE SCAN */
async function startScan(){
  await startCamera();
  scanText.innerText="Scanning wajah...";
  scanSound.currentTime=0;
  scanSound.play().catch(()=>{});

  setTimeout(()=>{
    scanSound.pause();
    scanText.innerText="Verifikasi berhasil ✔";
    stream.getTracks().forEach(t=>t.stop());
    setTimeout(()=>{
      loginBox.style.display="none";
      menuBox.style.display="block";
    },700);
  },3000);
}

/* LOGOUT */
function logout(){
  menuBox.style.display="none";
  loginBox.style.display="block";
}
</script>

</body>
</html>
