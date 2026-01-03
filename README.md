<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<meta name="theme-color" content="#020617">
<meta name="mobile-web-app-capable" content="yes">

<title>PREMIUM REwad – Scratch & Redeem</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif;user-select:none;-webkit-tap-highlight-color:transparent;}
body{min-height:100vh;background:linear-gradient(180deg,#020617,#0f172a);color:#fff;overflow-x:hidden;}

.bg-glow{position:fixed;width:500px;height:500px;background:radial-gradient(circle,#38bdf8,transparent 70%);filter:blur(120px);opacity:.22;top:-90px;left:50%;transform:translateX(-50%);z-index:-1;}

.wrapper{max-width:420px;margin:auto;padding:14px;}

.ad{background:rgba(255,255,255,.05);border:1px dashed rgba(255,255,255,.2);border-radius:14px;padding:14px;text-align:center;font-size:12px;color:#cbd5f5;margin:12px 0;}

.promo-buttons{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:10px 0;}
.promo-btn{display:block;text-decoration:none;text-align:center;padding:14px 10px;border-radius:14px;font-size:14px;font-weight:700;color:#fff;background:linear-gradient(135deg,#ec4899,#8b5cf6);box-shadow:0 0 18px rgba(236,72,153,.6);animation:pulse 1.4s infinite;}
@keyframes pulse{0%{transform:scale(1)}50%{transform:scale(1.08)}100%{transform:scale(1)}}

.container{background:linear-gradient(180deg,rgba(255,255,255,.08),rgba(255,255,255,.02));border:1px solid rgba(255,255,255,.15);backdrop-filter:blur(18px);padding:20px;border-radius:22px;box-shadow:0 30px 70px rgba(0,0,0,.6);text-align:center;}

.logo{font-size:22px;font-weight:700;}
.tagline{font-size:12px;color:#cbd5f5;margin:10px 0 14px;}

.card{position:relative;height:165px;border-radius:18px;overflow:hidden;background:linear-gradient(135deg,#fde68a,#f59e0b);}
.code{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:24px;font-weight:700;color:#111;letter-spacing:3px;}
canvas{position:absolute;inset:0;}

.info{margin:12px 0;font-size:12px;color:#cbd5f5;}
.actions{display:none;gap:8px;margin-top:8px;}
.actions button{flex:1;padding:12px;border:none;border-radius:12px;font-size:14px;font-weight:700;}
.copy{background:#22c55e;color:#052e16;}
.new{background:#3b82f6;color:#fff;}

.footer{text-align:center;font-size:11px;color:#94a3b8;margin:14px 0;}

.confetti{position:fixed;width:8px;height:8px;top:-10px;animation:fall linear forwards;}
@keyframes fall{to{transform:translateY(110vh) rotate(720deg);opacity:0}}
</style>
</head>

<body>

<div class="bg-glow"></div>

<div class="wrapper">

    <!-- Header -->
    <div class="container">
        <div class="logo">Premium Rewards</div>
         </div>

    <!-- Top Ad -->
    <div class="ad">Ad Space (Header Banner)</div>

    <!-- Top Buttons -->
    <div class="promo-buttons">
        <a href="https://otieu.com/4/10373293" class="promo-btn">Get Bonus</a>
        <a href="https://otieu.com/4/10394006" class="promo-btn">Claim Reward</a>
    </div>

    <!-- Scratch Card -->
    <div class="container">
        <div class="card">
            <div class="code" id="redeemCode">K9X7-Q2P8-MZ4</div>
            <canvas id="scratch"></canvas>
        </div>
        <div class="info">Scratch to reveal 🎉</div>
        <div class="actions" id="actions">
            <button class="copy" onclick="copyCode()">Copy</button>
            <button class="new" onclick="resetScratch()">Retry</button>
        </div>
    </div>

    <!-- Middle Ad -->
    <div class="ad">Ad Space (Native)</div>

    <!-- Bottom Buttons -->
    <div class="promo-buttons">
        <a href="https://otieu.com/4/10373356" class="promo-btn">Instant Win</a>
        <a href="https://otieu.com/4/10411656" class="promo-btn">Daily Offer</a>
    </div>

    <!-- Lucky Spin Button -->
    <div style="margin:10px 0;">
        <a href="https://otieu.com/4/10411656" class="promo-btn" style="width:100%;">Real Lucky Royal Spin</a>
    </div>

    <!-- Bottom Ad -->
    <div class="ad">Ad Space (Footer Banner)</div>
</div>

<script>
const canvas=document.getElementById("scratch");
const ctx=canvas.getContext("2d");
const card=document.querySelector(".card");
const actions=document.getElementById("actions");

function initScratch(){
    canvas.width=card.offsetWidth;
    canvas.height=card.offsetHeight;
    ctx.globalCompositeOperation="source-over";
    ctx.fillStyle="#9ca3af";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.globalCompositeOperation="destination-out";
    actions.style.display="none";
}
initScratch();

let scratching=false,done=false,count=0;

canvas.addEventListener("touchstart",()=>scratching=true,{passive:true});
canvas.addEventListener("touchend",()=>scratching=false);
canvas.addEventListener("touchmove",e=>{
    if(!scratching) return;
    const r=canvas.getBoundingClientRect();
    const x=e.touches[0].clientX - r.left;
    const y=e.touches[0].clientY - r.top;
    ctx.beginPath();
    ctx.arc(x,y,20,0,Math.PI*2);
    ctx.fill();
    if(navigator.vibrate) navigator.vibrate(8);
    count++;
    if(count>90 && !done){
        done=true;
        actions.style.display="flex";
        showConfetti();
    }
},{passive:true});

function showConfetti(){
    for(let i=0;i<70;i++){
        const c=document.createElement("div");
        c.className="confetti";
        c.style.left=Math.random()*100+"vw";
        c.style.background=`hsl(${Math.random()*360},90%,60%)`;
        c.style.animationDuration=2+Math.random()*2+"s";
        document.body.appendChild(c);
        setTimeout(()=>c.remove(),4000);
    }
}

function copyCode(){
    navigator.clipboard.writeText(document.getElementById("redeemCode").innerText);
    if(navigator.vibrate) navigator.vibrate(60);
    alert("Code Copied!");
}

function resetScratch(){
    const chars="ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
    let code="";
    for(let i=0;i<12;i++){
        code+=chars[Math.floor(Math.random()*chars.length)];
        if(i==3||i==7) code+="-";
    }
    document.getElementById("redeemCode").innerText=code;
    count=0;done=false;
    initScratch();
}
</script>

</body>
</html>
