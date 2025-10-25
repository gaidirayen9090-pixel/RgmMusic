# RgmMusic
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RGM rvayen</title>
<link rel="stylesheet" href="style.css">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
</head>
<body>
<div class="background"></div>

<div class="container">
  <header>
    <h1>RGM rvayen</h1>
    <p>فنان راب جديد من قفصة | Rap Artist from Gafsa</p>
  </header>

  <section class="music-section">
    <h2>أغنيتي الجديدة</h2>
    <div id="player"></div>
    <button id="playBtn">▶ تشغيل / إيقاف</button>
    <canvas id="waveCanvas"></canvas>
    <p>قريبًا: قصة "رحلة محارب" على YouTube</p>
  </section>

  <section class="links">
    <a href="https://www.instagram.com/rgm__phinix?igsh=MTN1OHE3Nm45eTBwMA==" target="_blank" class="icon insta">Instagram</a>
    <a href="https://youtube.com/@rgmrvayen?si=Q051aRJVpFob5Uwl" target="_blank" class="icon yt">YouTube</a>
    <a href="#" class="icon spotify">Spotify (قريبًا)</a>
  </section>
</div>

<script src="https://www.youtube.com/iframe_api"></script>
<script src="script.js"></script>
</body>
</html>
* { margin:0; padding:0; box-sizing:border-box; }

body, html {
  height: 100%;
  font-family: 'Orbitron', sans-serif;
  background: #000;
  overflow-x: hidden;
}

.background {
  position: fixed;
  width: 100%;
  height: 100%;
  background: linear-gradient(270deg, #0f0c29, #302b63, #24243e);
  background-size: 600% 600%;
  animation: gradientBG 20s ease infinite;
  z-index: -1;
}

@keyframes gradientBG {
  0%{background-position:0% 50%}
  50%{background-position:100% 50%}
  100%{background-position:0% 50%}
}

.container {
  text-align: center;
  color: #fff;
  padding: 40px 20px;
}

header h1 {
  font-size: 3rem;
  color: #f39c12;
  text-shadow: 0 0 10px #f39c12, 0 0 20px #f39c12;
  margin-bottom: 10px;
}

header p {
  font-size: 1.2rem;
  color: #fff;
  text-shadow: 0 0 5px #f39c12;
}

.music-section {
  margin: 40px 0;
}

button {
  padding: 12px 30px;
  font-size: 1rem;
  background: #f39c12;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  color: #000;
  box-shadow: 0 0 20px #f39c12;
  transition: all 0.3s ease;
}

button:hover { transform: scale(1.1); background:#e67e22; }

canvas {
  display: block;
  margin: 20px auto;
  width: 90%;
  max-width: 700px;
  height: 150px;
  border-radius: 15px;
  box-shadow: 0 0 20px #f39c12;
}

.links {
  margin-top: 30px;
}

.links a {
  display:inline-block;
  text-decoration:none;
  color:#fff;
  font-size:1.5rem;
  margin:10px;
  padding:10px 25px;
  border:2px solid #fff;
  border-radius:50px;
  transition: all 0.3s ease;
}

.links a:hover {
  background:#f39c12;
  border-color:#f39c12;
  color:#000;
  transform: scale(1.1);
}

.insta { background:#E1306C; border-color:#E1306C; }
.yt { background:#FF0000; border-color:#FF0000; }
.spotify { background:#1DB954; border-color:#1DB954; }
let player;
let isPlaying = false;

const canvas = document.getElementById('waveCanvas');
const ctx = canvas.getContext('2d');
canvas.width = canvas.offsetWidth;
canvas.height = canvas.offsetHeight;

// YouTube Player
function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
        height: '360',
        width: '640',
        videoId: 'EDxb1X1h--Y',
        playerVars: { 'autoplay': 0, 'controls': 0 },
        events: { 'onReady': onPlayerReady }
    });
}

function onPlayerReady(event) {
    drawWave();
}

document.getElementById('playBtn').addEventListener('click', ()=>{
    if(!isPlaying){
        player.playVideo();
        isPlaying=true;
    }else{
        player.pauseVideo();
        isPlaying=false;
    }
});

// Simple wave animation
function drawWave(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    let time = new Date().getTime() * 0.002;
    ctx.beginPath();
    for(let x=0;x<canvas.width;x++){
        let y = canvas.height/2 + Math.sin(x*0.02 + time)*30;
        ctx.lineTo(x,y);
    }
    ctx.strokeStyle="#f39c12";
    ctx.lineWidth=2;
    ctx.stroke();
    requestAnimationFrame(drawWave);
}
