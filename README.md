<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pengingat Ramadan 2026 • CodeMuna</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Amiri:wght@700&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#020617;
  --card:#020617cc;
  --text:#e5e7eb;
  --accent:#facc15;
  --green:#22c55e;
}
.light{
  --bg:#f8fafc;
  --card:#ffffff;
  --text:#020617;
}
*{margin:0;padding:0;box-sizing:border-box}
body{
  font-family:Poppins,sans-serif;
  background:radial-gradient(circle at top,#022c22,var(--bg));
  color:var(--text);
  transition:.4s;
}
.container{max-width:430px;margin:auto;padding:20px}
.card{
  background:var(--card);
  border-radius:22px;
  padding:24px;
  box-shadow:0 20px 40px rgba(0,0,0,.4);
}
.top{display:flex;justify-content:flex-end}
.toggle{cursor:pointer;font-size:20px}
h1{
  font-family:Amiri,serif;
  color:var(--accent);
  text-align:center;
  font-size:30px;
}
.sub{text-align:center;font-size:13px;opacity:.8;margin-bottom:16px}
.countdown{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;margin:16px 0;
}
.box{
  background:linear-gradient(160deg,#064e3b,#0f766e);
  border-radius:14px;padding:12px;text-align:center;color:#fff
}
.box h2{font-size:22px}
select{
  width:100%;padding:12px;border-radius:14px;border:none;
  margin:10px 0;font-size:14px
}
.section{margin-top:20px}
.section h3{text-align:center;margin-bottom:10px;color:var(--green)}
.list{background:rgba(0,0,0,.15);border-radius:14px;padding:12px}
.light .list{background:#f1f5f9}
.row{
  display:flex;justify-content:space-between;
  padding:8px 0;border-bottom:1px solid #ffffff12
}
.row:last-child{border:none}
.link-btn{
  display:block;margin-top:22px;padding:14px;
  text-align:center;text-decoration:none;font-weight:600;
  border-radius:16px;color:#020617;
  background:linear-gradient(160deg,#fde047,#facc15)
}
footer{text-align:center;margin-top:16px;font-size:12px;opacity:.6}
.status{
  text-align:center;font-size:12px;margin-top:6px;opacity:.7
}
</style>
</head>

<body>
<div class="container">
<div class="card">

<div class="top">
  <div class="toggle" onclick="toggleMode()">🌙</div>
</div>

<h1>🕌 Ramadan 1447 H</h1>
<div class="sub">
Pengingat Ramadan 2026 • Auto Lokasi GPS<br>
by <b>CodeMuna</b>
</div>

<div class="countdown">
  <div class="box"><h2 id="d">0</h2>Hari</div>
  <div class="box"><h2 id="h">0</h2>Jam</div>
  <div class="box"><h2 id="m">0</h2>Menit</div>
  <div class="box"><h2 id="s">0</h2>Detik</div>
</div>

<div class="section">
<h3>📍 Lokasi</h3>
<select id="kota"></select>
<div class="status" id="statusLokasi">Menentukan lokasi…</div>
</div>

<div class="section">
<h3>⏰ Jadwal Sholat Hari Ini</h3>
<div class="list">
  <div class="row"><span>Subuh</span><b id="subuh">--:--</b></div>
  <div class="row"><span>Dzuhur</span><b id="dzuhur">--:--</b></div>
  <div class="row"><span>Ashar</span><b id="ashar">--:--</b></div>
  <div class="row"><span>Maghrib</span><b id="maghrib">--:--</b></div>
  <div class="row"><span>Isya</span><b id="isya">--:--</b></div>
</div>
</div>

<a class="link-btn" href="https://droid10.my.id/" target="_blank">
🔗 Kunjungi Link Utama
</a>

<footer>© 2026 • Pengingat Ramadan • CodeMuna</footer>
</div>
</div>

<script>
// ===== MODE
const body=document.body,toggle=document.querySelector(".toggle");
if(localStorage.mode==="light"){body.classList.add("light");toggle.textContent="☀️";}
function toggleMode(){
 body.classList.toggle("light");
 const l=body.classList.contains("light");
 toggle.textContent=l?"☀️":"🌙";
 localStorage.mode=l?"light":"dark";
}

// ===== DATA KOTA (KOORDINAT)
const kotaList=[
 {n:"Jakarta",lat:-6.2,lon:106.8},
 {n:"Bandung",lat:-6.9,lon:107.6},
 {n:"Surabaya",lat:-7.25,lon:112.75},
 {n:"Medan",lat:3.59,lon:98.67},
 {n:"Makassar",lat:-5.14,lon:119.41},
 {n:"Semarang",lat:-6.97,lon:110.42},
 {n:"Palembang",lat:-2.99,lon:104.75},
 {n:"Padang",lat:-0.94,lon:100.35},
 {n:"Pekanbaru",lat:0.53,lon:101.44},
 {n:"Banjarmasin",lat:-3.32,lon:114.59},
 {n:"Kendari",lat:-3.99,lon:122.51},
 {n:"Kabupaten Muna",lat:-4.83,lon:122.72}
];

const kotaSel=document.getElementById("kota");
kotaList.forEach((k,i)=>{
 let o=document.createElement("option");
 o.value=i;o.textContent=k.n;
 kotaSel.appendChild(o);
});

// ===== HITUNG JARAK
function jarak(lat1,lon1,lat2,lon2){
 const R=6371;
 const dLat=(lat2-lat1)*Math.PI/180;
 const dLon=(lon2-lon1)*Math.PI/180;
 const a=Math.sin(dLat/2)**2+
 Math.cos(lat1*Math.PI/180)*Math.cos(lat2*Math.PI/180)*
 Math.sin(dLon/2)**2;
 return R*(2*Math.atan2(Math.sqrt(a),Math.sqrt(1-a)));
}

// ===== AUTO GPS
if(navigator.geolocation){
 navigator.geolocation.getCurrentPosition(pos=>{
  let {latitude,longitude}=pos.coords;
  let min=9999,idx=0;
  kotaList.forEach((k,i)=>{
   let d=jarak(latitude,longitude,k.lat,k.lon);
   if(d<min){min=d;idx=i}
  });
  kotaSel.value=idx;
  statusLokasi.innerText="Lokasi otomatis terdeteksi";
  loadSholat();
 },()=>{
  statusLokasi.innerText="GPS ditolak, pilih manual";
 });
}else{
 statusLokasi.innerText="GPS tidak tersedia";
}

// ===== RAMADAN COUNTDOWN
const ramadan=new Date("2026-02-18T18:00:00").getTime();
setInterval(()=>{
 let now=Date.now(),x=ramadan-now;
 if(x<0)return;
 d.innerText=Math.floor(x/86400000);
 h.innerText=Math.floor(x%86400000/3600000);
 m.innerText=Math.floor(x%3600000/60000);
 s.innerText=Math.floor(x%60000/1000);
},1000);

// ===== SHOLAT
async function loadSholat(){
 let k=kotaList[kotaSel.value];
 let r=await fetch(`https://api.aladhan.com/v1/timings?latitude=${k.lat}&longitude=${k.lon}&method=20`);
 let t=(await r.json()).data.timings;
 subuh.innerText=t.Fajr;
 dzuhur.innerText=t.Dhuhr;
 ashar.innerText=t.Asr;
 maghrib.innerText=t.Maghrib;
 isya.innerText=t.Isha;
}
kotaSel.onchange=loadSholat;
loadSholat();
</script>

</body>
</html>
