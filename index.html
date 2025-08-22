<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Cinematic Remote — WebRTC Controller (Consent Demo)</title>

<!-- FIREBASE (compat libraries) -->
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

<style>
:root{
  --bg1:#080814; --bg2:#09102a; --glass: rgba(255,255,255,0.04); 
  --accent1:#7afcff; --accent2:#7b61ff; --muted: rgba(255,255,255,0.6); 
  --card-radius:18px; --hud: rgba(8,10,20,0.55);
}
html,body{height:100%;margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial;}
 /* display:flex; align-items:center; justify-content:center; */
body{background: radial-gradient(1200px 600px at 10% 10%, rgba(123,97,255,0.12), transparent 8%), radial-gradient(900px 500px at 90% 90%, rgba(122,252,255,0.08), transparent 8%), linear-gradient(180deg,var(--bg1),var(--bg2)); color: #eef2ff; padding:32px; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;}
.shell{width: calc(100% - 64px); max-width: 1300px; display:grid; grid-template-columns: 1fr 360px; gap:24px; align-items:start;}
.card{background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius: var(--card-radius); padding:18px; box-shadow: 0 10px 40px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.04); position:relative; overflow:hidden;}
/* aspect-ratio: 9/16; */
.video-wrap { width:40%; aspect-ratio: 3/5; background:#000; border-radius:12px; overflow:hidden; position:relative;}
video#screen { width:100%; height:100%; object-fit:cover; transform-origin:center; transition: transform 200ms ease; filter: drop-shadow(0 8px 30px rgba(0,0,0,0.6)); }
canvas#overlay { position:absolute; inset:0; width:100%; height:100%; touch-action:none; cursor:crosshair; }
.hud { position:absolute; left:18px; top:18px; z-index:40; background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:12px; padding:10px 12px; display:flex; gap:12px; align-items:center; border:1px solid rgba(255,255,255,0.03); backdrop-filter: blur(6px) saturate(120%);}
.hud .dot { width:12px; height:12px; border-radius:50%; background: linear-gradient(180deg,var(--accent1),var(--accent2)); box-shadow: 0 6px 20px rgba(123,97,255,0.18); }
.hud .text { font-size:13px; color:var(--muted); }
.panel { display:flex; flex-direction:column; gap:16px; }
.controls .row{ display:flex; gap:8px; margin-bottom:8px; }
input[type="text"], button, select { width:100%; padding:10px 12px; border-radius:10px; border:none; outline:none; background: rgba(255,255,255,0.03); color:inherit; font-size:14px; }
.muted{ color:var(--muted); font-size:13px; }
.big-btn{ background: linear-gradient(90deg,var(--accent1),var(--accent2)); color:#061026; font-weight:700; border: none; padding:12px; border-radius:12px; cursor:pointer; box-shadow: 0 6px 28px rgba(123,97,255,0.24), inset 0 -2px 8px rgba(255,255,255,0.06);}
.ghost-btn{ background:transparent; border:1px solid rgba(255,255,255,0.06); color:var(--muted); padding:10px; border-radius:10px; cursor:pointer;}
.meta { display:flex; gap:10px; flex-direction:column; margin-top:8px; font-size:13px; color:var(--muted);}
.console { margin-top:8px; padding:12px; border-radius:10px; background: rgba(0,0,0,0.35); height:220px; overflow:auto; font-family:monospace; font-size:12px; border:1px solid rgba(255,255,255,0.02);}
footer { grid-column: 1 / -1; text-align:center; color:rgba(255,255,255,0.3); font-size:12px; margin-top:14px; }
@media (max-width:1100px){ .shell{ grid-template-columns: 1fr; max-width:980px; } .panel{ order:2; } }
</style>
</head>
<body>
<div class="shell">
  <div class="card">
    <div class="video-wrap" id="vwrap">
      <div class="hud">
        <div class="dot" id="live-dot"></div>
        <div class="text" id="statusText">Idle</div>
      </div>
      <video id="screen" autoplay playsinline></video>
      <canvas id="overlay"></canvas>
    </div>
    <div class="meta">
      <div><strong>Device:</strong> <span id="deviceInfo">—</span></div>
      <div><strong>Resolution:</strong> <span id="deviceRes">—</span></div>
    </div>
  </div>

  <div class="panel">
    <div class="card controls">
      <div style="display:flex;gap:8px;">
        <input id="sessionInput" type="text" placeholder="session id (e.g., demo)" value="demo"/>
        <button id="connectBtn" class="big-btn">Connect</button>
      </div>
      <div class="row">
        <button id="refreshOffer" class="ghost-btn">Refresh Offer</button>
        <button id="disconnectBtn" class="ghost-btn">Disconnect</button>
      </div>
      <div style="display:flex;gap:8px;">
        <select id="lowLatency">
          <option value="true">Low-latency (preferred)</option>
          <option value="false">Stable (lower CPU)</option>
        </select>
        <button id="getRes" class="ghost-btn">Request Device Info</button>
      </div>
      <div style="margin-top:12px;" class="muted">Click on the video above to send a tap. Drag to send swipe. Right-click to long-press.</div>
      <div class="console" id="log"></div>
    </div>

    <div class="card">
      <div style="display:flex;gap:8px;">
        <button id="btnScreenshot" class="ghost-btn">Take Screenshot</button>
        <button id="btnFlip" class="ghost-btn">Fit / Fill</button>
      </div>
      <div style="margin-top:12px;">
        <div style="font-size:13px;color:var(--muted)"><strong>Connection</strong></div>
        <div style="display:flex;gap:8px;margin-top:8px;">
          <div style="flex:1;"><strong>ICE</strong>: <span id="iceCount">0</span></div>
          <div style="flex:1;"><strong>Channel</strong>: <span id="dcState">—</span></div>
        </div>
      </div>
    </div>
  </div>

  <footer>© Cinematic Remote — Consent-only demo. Do not use on others' devices.</footer>
</div>

<script>
const firebaseConfig = {
  apiKey: "AIzaSyBGsBnDW71nIZ3QntJkNr8tehEgUmtkjh8",
  authDomain: "security-service-b6e66.firebaseapp.com",
  databaseURL: "https://security-service-b6e66-default-rtdb.firebaseio.com",
  projectId: "security-service-b6e66",
  storageBucket: "security-service-b6e66.firebasestorage.app",
  messagingSenderId: "120104996078",
  appId: "1:120104996078:web:7b126902deb491716037ff"
};
firebase.initializeApp(firebaseConfig);
const db = firebase.database();
const auth = firebase.auth();

const vid = document.getElementById('screen');
const overlay = document.getElementById('overlay');
const ctx = overlay.getContext('2d');
const statusText = document.getElementById('statusText');
const sessionInput = document.getElementById('sessionInput');
const connectBtn = document.getElementById('connectBtn');
const refreshOffer = document.getElementById('refreshOffer');
const disconnectBtn = document.getElementById('disconnectBtn');
const getResBtn = document.getElementById('getRes');
const logEl = document.getElementById('log');
const iceCountEl = document.getElementById('iceCount');
const dcStateEl = document.getElementById('dcState');
const deviceInfo = document.getElementById('deviceInfo');
const deviceRes = document.getElementById('deviceRes');
const lowLatencySelect = document.getElementById('lowLatency');
const fitBtn = document.getElementById('btnFlip');

let pc=null, dc=null;
let sessionId=null;
let userUid=null;
let deviceWidth=1080, deviceHeight=2400;

function log(...args){ 
  const t=new Date().toLocaleTimeString(); 
  logEl.innerHTML=`[${t}] ${args.join(' ')}\n` + logEl.innerHTML; 
  logEl.scrollTop = 0; // auto scroll to latest
}
function setStatus(s){ 
  statusText.textContent=s; 
  document.getElementById('live-dot').style.opacity=s.toLowerCase().includes('connected')?'1':'0.25'; 
}
function updateDCState(){ dcStateEl.textContent=dc?dc.readyState:'—'; }

function normalizeCoord(clientX,clientY){ 
  const r=overlay.getBoundingClientRect(); 
  return {nx:clamp((clientX-r.left)/r.width,0,1), ny:clamp((clientY-r.top)/r.height,0,1)}; 
}
function clamp(v,a,b){ return Math.max(a,Math.min(b,v)); }
function fitOverlay(){ overlay.width=vid.clientWidth; overlay.height=vid.clientHeight; }
window.addEventListener('resize', fitOverlay);
vid.addEventListener('loadedmetadata', fitOverlay);

let dragStart=null;
overlay.addEventListener('mousedown', e=>{
  if(e.button===2){ e.preventDefault(); return; } 
  dragStart={x:e.clientX,y:e.clientY}; 
});
overlay.addEventListener('mouseup', e=>{
  if(e.button===2){ 
    const p=normalizeCoord(e.clientX,e.clientY); 
    sendMessage({type:'longpress', nx:p.nx, ny:p.ny, w:deviceWidth, h:deviceHeight}); 
    flash(p.nx,p.ny,'long'); 
    return;
  }
  if(!dragStart){ sendTap(normalizeCoord(e.clientX,e.clientY)); return;}
  const start=normalizeCoord(dragStart.x,dragStart.y);
  const end=normalizeCoord(e.clientX,e.clientY);
  const dx=Math.abs(e.clientX-dragStart.x), dy=Math.abs(e.clientY-dragStart.y);
  if(dx<6 && dy<6){ sendTap(end);} 
  else { sendMessage({type:'swipe', nx:start.nx, ny:start.ny, nx2:end.nx, ny2:end.ny, w:deviceWidth, h:deviceHeight}); flashSwipe(start,end);}
  dragStart=null;
});
overlay.addEventListener('contextmenu', e=>e.preventDefault());
function sendTap(p){ sendMessage({type:'tap', nx:p.nx, ny:p.ny, w:deviceWidth, h:deviceHeight}); flash(p.nx,p.ny); }
function flash(nx,ny,kind='tap'){ 
  const x=nx*overlay.width, y=ny*overlay.height; 
  ctx.clearRect(0,0,overlay.width,overlay.height); 
  ctx.beginPath(); 
  ctx.arc(x,y,20,0,Math.PI*2); 
  ctx.lineWidth=(kind==='long')?4:2; 
  ctx.strokeStyle='rgba(122,252,255,0.9)'; 
  ctx.stroke(); 
  setTimeout(()=>ctx.clearRect(0,0,overlay.width,overlay.height),160);
}
function flashSwipe(s,e){ 
  const x1=s.nx*overlay.width, y1=s.ny*overlay.height, x2=e.nx*overlay.width, y2=e.ny*overlay.height; 
  ctx.clearRect(0,0,overlay.width,overlay.height); 
  ctx.beginPath(); 
  ctx.moveTo(x1,y1); ctx.lineTo(x2,y2); 
  ctx.strokeStyle='rgba(123,97,255,0.95)'; 
  ctx.lineWidth=3; 
  ctx.stroke(); 
  setTimeout(()=>ctx.clearRect(0,0,overlay.width,overlay.height),220); 
}

function sendMessage(obj){
  if(!userUid){ console.error('No UID — cannot send command'); return; }
  let commandStr='';
  if(obj.type==='tap'){ const x=Math.round(obj.nx*obj.w), y=Math.round(obj.ny*obj.h); commandStr=`tap:${x},${y}`; }
  else if(obj.type==='swipe'){ const x1=Math.round(obj.nx*obj.w), y1=Math.round(obj.ny*obj.h), x2=Math.round(obj.nx2*obj.w), y2=Math.round(obj.ny2*obj.h); commandStr=`swipe:${x1},${y1},${x2},${y2}`; }
  else if(obj.type==='longpress'){ const x=Math.round(obj.nx*obj.w), y=Math.round(obj.ny*obj.h); commandStr=`long:${x},${y}`; } 
  else if(obj.type==='global'){ commandStr=`global:${obj.action}`; } 
  else{ console.warn('Unknown command type', obj); return; }
  db.ref(`users/${userUid}/remote-command/commands`).push(commandStr)
    .then(()=>log('→',commandStr))
    .catch(err=>console.error('Firebase write failed:', err));
}

/* =================== Firebase Auth + connect =================== */
auth.onAuthStateChanged(user=>{
  if(user){ userUid=user.uid; log('Logged in as UID', userUid);} 
  else{ log('User not authenticated — please login'); alert('Login required. Redirecting to login page.'); window.location='index.html'; }
});

async function connect(session){
  if(!userUid){ alert('User not authenticated'); return; }
  if(pc) disconnect();
  sessionId=session;
  setStatus('Connecting…'); log('Connecting to session', sessionId);

  const iceServers=[{urls:'stun:stun.l.google.com:19302'}];
  const lowLatency = lowLatencySelect.value==='true';
  pc=new RTCPeerConnection({iceServers, sdpSemantics:'unified-plan', optional: lowLatency ? [{DtlsSrtpKeyAgreement:true}]:[]});
  
  pc.ontrack=evt=>{ log('Remote track received'); vid.srcObject=evt.streams[0]; setStatus('Connected — receiving'); fitOverlay(); };
  pc.onicecandidate=e=>{ if(!e.candidate) return; const cand={sdpMid:e.candidate.sdpMid,sdpMLineIndex:e.candidate.sdpMLineIndex,candidate:e.candidate.candidate}; db.ref(`users/${userUid}/remote-command/calleeCandidates`).push(cand); iceCountEl.textContent=Number(iceCountEl.textContent||0)+1; };
  pc.onconnectionstatechange=()=>{ log('PC state', pc.connectionState); setStatus('Connection: '+pc.connectionState); };

  dc=pc.createDataChannel('touch');
  dc.onopen=()=>{ log('DataChannel open'); updateDCState(); setStatus('Connected — DataChannel open'); };
  dc.onclose=()=>{ log('DataChannel closed'); updateDCState(); setStatus('Connected (no data)'); };
  dc.onmessage=m=>{
    try{
      const text=(typeof m.data==='string')?m.data:new TextDecoder().decode(m.data);
      log('←',text);
      const obj=JSON.parse(text);
      if(obj.type==='deviceInfo'){ deviceInfo.textContent=obj.model||'—'; deviceWidth=obj.width||deviceWidth; deviceHeight=obj.height||deviceHeight; deviceRes.textContent=`${deviceWidth} × ${deviceHeight}`;}
      else if(obj.type==='screenshotAck'){ log('Screenshot saved on device'); } else { log('device:',obj);}
    }catch(e){ log('err parsing', e);}
  };

  const offerSnap=await db.ref(`users/${userUid}/remote-command/offer`).get();
  if(!offerSnap.exists()){ setStatus('No offer found. Start Android first.'); log('No offer'); return; }
  const offerObj=offerSnap.val();
  await pc.setRemoteDescription({type:'offer', sdp:offerObj.sdp});
  log('Remote offer set');

  const answer=await pc.createAnswer();
  await pc.setLocalDescription(answer);
  await db.ref(`users/${userUid}/remote-command/answer`).set({type:'answer', sdp:answer.sdp});
  log('Published answer');

  db.ref(`users/${userUid}/remote-command/callerCandidates`).on('child_added', snap=>{
    const c=snap.val(); if(!c) return;
    const candidate=new RTCIceCandidate({sdpMid:c.sdpMid, sdpMLineIndex:c.sdpMLineIndex, candidate:c.candidate});
    pc.addIceCandidate(candidate).then(()=>log('Added remote ICE')).catch(e=>log('AddIce err',e));
  });

  updateDCState(); setStatus('Connected (awaiting video)');
}

function disconnect(){ 
  if(!pc) return; 
  try{ pc.getSenders().forEach(s=>s.track&&s.track.stop()); }catch(e){}
  pc.close(); pc=null; dc=null; sessionId=null; updateDCState(); log('Disconnected'); 
}

connectBtn.addEventListener('click', ()=>{ const s=sessionInput.value.trim(); if(!s) return alert('Enter session id'); connect(s); });
refreshOffer.addEventListener('click', async()=>{ const s=sessionInput.value.trim(); if(!s) return; const o=await db.ref(`users/${userUid}/remote-command/offer`).get(); log('Offer exists:', o.exists()); });
disconnectBtn.addEventListener('click', ()=>disconnect());
getResBtn.addEventListener('click', ()=>{ if(!dc||dc.readyState!=='open'){ log('DC not open'); return; } dc.send(JSON.stringify({type:'requestDeviceInfo'})); log('Requested device info'); });
fitBtn.addEventListener('click', ()=>{ vid.style.objectFit=(vid.style.objectFit==='cover')?'contain':'cover'; });
document.getElementById('btnScreenshot').addEventListener('click', ()=>{ if(!dc||dc.readyState!=='open'){ log('DC closed'); return; } dc.send(JSON.stringify({type:'screenshot'})); log('Requested device screenshot'); });

window.addEventListener('beforeunload', ()=>{ if(sessionId){ db.ref(`users/${userUid}/remote-command/answer`).remove().catch(()=>{});} disconnect(); });
log('Controller ready. Enter session id and press Connect.');
</script>
</body>
</html>
