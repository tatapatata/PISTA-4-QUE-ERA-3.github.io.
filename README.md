<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Pinta por números — Panda rojo & Mapache</title>
<meta name="description" content="Pinta por números: panda rojo y mapache. Completa el lienzo y recibe la pista (playlist)." />
<style>
  :root{
    --bg:#081126; --panel:#0b1324; --text:#e6eefc; --muted:#98a8c7;
    --accent:#f6b26b; --ok:#3ee6a0; --bad:#ff7b7b;
  }
  *{box-sizing:border-box}
  body{
    margin:0; font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    background:linear-gradient(180deg,#071025 0%, #071428 100%); color:var(--text); -webkit-font-smoothing:antialiased;
  }
  header{padding:18px 16px;text-align:center}
  h1{margin:0;font-size:clamp(18px,3.8vw,28px)}
  p.lead{margin:8px 0 0;color:var(--muted);max-width:880px;margin-left:auto;margin-right:auto}
  .wrap{max-width:980px;margin:18px auto;padding:0 14px}
  .topbar{display:flex;gap:10px;align-items:center;justify-content:center;margin:12px 0 18px}
  .board{background:var(--panel);border-radius:16px;padding:12px;box-shadow:0 8px 30px rgba(2,6,23,.6)}
  .svgwrap{max-width:820px;margin:0 auto;touch-action:none}
  svg{width:100%;height:auto;display:block}
  .controls{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px}
  .chip{width:46px;height:46px;border-radius:50%;display:grid;place-items:center;font-weight:800;color:#031226;border:cursor:pointer;border:2px solid rgba(255,255,255,.06);box-shadow:0 4px 18px rgba(2,6,23,.5)}
  .chip[data-selected="true"]{outline:3px solid var(--accent);box-shadow:0 10px 30px rgba(0,0,0,.6)}
  .legend{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:8px;margin-top:12px}
  .legendItem{display:flex;gap:10px;align-items:center;padding:8px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,.02), transparent)}
  .sw{width:20px;height:20px;border-radius:50%;border:1px solid rgba(0,0,0,.15)}
  .bar{display:flex;gap:8px;justify-content:center;margin-top:12px}
  button{background:#0f1a33;border:1px solid #20304b;color:var(--text);padding:10px 12px;border-radius:10px;cursor:pointer;font-weight:700}
  button:hover{filter:brightness(1.07)}
  #msg{min-height:26px;text-align:center;margin:12px 0;color:var(--muted)}
  /* modal/QR */
  .modal{position:fixed;inset:0;display:grid;place-items:center;background:rgba(4,6,12,.7);z-index:60;opacity:0;pointer-events:none;transition:opacity .18s}
  .modal.show{opacity:1;pointer-events:auto}
  .card{background:linear-gradient(180deg,#071428,#071226);border-radius:14px;padding:18px;border:1px solid rgba(255,255,255,.06);max-width:420px;text-align:center}
  .qr{width:260px;height:260px;margin:10px auto;background:#fff;padding:10px;border-radius:10px}
  a.openBtn{display:inline-block;margin-top:10px;padding:10px 14px;border-radius:12px;background:var(--accent);color:#04122b;text-decoration:none;font-weight:800}
  @media (max-width:760px){
    .chip{width:40px;height:40px}
    .qr{width:200px;height:200px}
  }
  /* zone defaults */
  .zone{fill:#ffffff;stroke:#001122;stroke-width:2;cursor:pointer}
  .zone.filled{stroke:#001018}
  .numText{font-weight:800;fill:#02102b;stroke:#fff;stroke-width:3px;font-size:14px;pointer-events:none}
</style>
</head>
<body>
<header>
  <h1>Pinta por números</h1>
  <p class="lead">Elige un número (color) y toca la zona con ese número. Cuando completes todo, recibirás la sorpresa: la playlist.</p>
</header>

<div class="wrap">
  <div class="topbar">
    <div style="background:#071226;padding:8px 12px;border-radius:12px">Lista de colores • Toca para elegir</div>
  </div>

  <div class="board" role="application" aria-label="Pinta por números">
    <div class="svgwrap" id="svgwrap">
      <!-- SVG 800x800: panda rojo (izq) y mapache (der). Zonas grandes y numeradas. -->
      <svg id="scene" viewBox="0 0 800 800" role="img" aria-labelledby="title desc">
        <title id="title">Panda rojo y mapache</title>
        <desc id="desc">Ilustración para colorear por números. Cada zona está marcada con su número.</desc>

        <!-- fondo -->
        <rect x="0" y="0" width="800" height="800" fill="transparent"></rect>

        <!-- suelo -->
        <rect class="zone" data-num="10" x="40" y="740" width="720" height="40"></rect>

        <!-- corazón central (no cuenta como número de cuerpo pero visible) -->
        <path d="M380 450c0-20 16-32 30-32 10 0 18 5 23 12 5-7 13-12 23-12 14 0 30 12 30 32 0 28-36 46-53 64-17-18-53-36-53-64z"
              class="zone" data-num="12" transform="translate(0,-10)"></path>

        <!-- === PANDA ROJO === (izquierda) -->
        <!-- cola -->
        <ellipse class="zone" data-num="1" cx="140" cy="640" rx="92" ry="36"></ellipse>
        <rect class="zone" data-num="2" x="80" y="610" width="44" height="40" rx="12"></rect>
        <rect class="zone" data-num="2" x="130" y="610" width="44" height="40" rx="12"></rect>

        <!-- cuerpo -->
        <ellipse class="zone" data-num="1" cx="250" cy="520" rx="120" ry="160"></ellipse>
        <!-- panza -->
        <ellipse class="zone" data-num="3" cx="250" cy="560" rx="72" ry="96"></ellipse>

        <!-- brazo derecho (mano que toma) -->
        <ellipse class="zone" data-num="1" cx="325" cy="470" rx="36" ry="64"></ellipse>

        <!-- cabeza -->
        <ellipse class="zone" data-num="1" cx="250" cy="320" rx="100" ry="92"></ellipse>
        <!-- máscara clara -->
        <ellipse class="zone" data-num="3" cx="250" cy="340" rx="72" ry="48"></ellipse>
        <!-- orejas -->
        <path class="zone" data-num="1" d="M190 240 C 200 190, 240 190, 240 240 Z"></path>
        <path class="zone" data-num="1" d="M310 240 C 300 190, 260 190, 260 240 Z"></path>
        <!-- orejas internas -->
        <path class="zone" data-num="4" d="M205 240 C 210 215, 230 215, 228 240 Z"></path>
        <path class="zone" data-num="4" d="M295 240 C 290 215, 270 215, 272 240 Z"></path>

        <!-- mejillas -->
        <circle class="zone" data-num="12" cx="215" cy="360" r="14"></circle>
        <circle class="zone" data-num="12" cx="285" cy="360" r="14"></circle>

        <!-- patitas -->
        <ellipse class="zone" data-num="8" cx="210" cy="700" rx="36" ry="22"></ellipse>
        <ellipse class="zone" data-num="8" cx="290" cy="700" rx="36" ry="22"></ellipse>

        <!-- === MAPACHE === (derecha) -->
        <!-- cola -->
        <ellipse class="zone" data-num="5" cx="660" cy="640" rx="92" ry="36"></ellipse>
        <rect class="zone" data-num="7" x="615" y="610" width="44" height="40" rx="12"></rect>
        <rect class="zone" data-num="7" x="665" y="610" width="44" height="40" rx="12"></rect>

        <!-- cuerpo -->
        <ellipse class="zone" data-num="5" cx="550" cy="520" rx="120" ry="160"></ellipse>
        <!-- panza -->
        <ellipse class="zone" data-num="9" cx="550" cy="560" rx="72" ry="96"></ellipse>

        <!-- brazo izquierdo (mano que toma) -->
        <ellipse class="zone" data-num="6" cx="475" cy="470" rx="36" ry="64"></ellipse>

        <!-- cabeza -->
        <ellipse class="zone" data-num="5" cx="550" cy="320" rx="100" ry="92"></ellipse>
        <!-- antifaz -->
        <path class="zone" data-num="7" d="M460 320 C 520 260, 580 260, 640 320 L 640 360 C 580 320, 520 320, 460 360 Z"></path>
        <!-- orejas -->
        <path class="zone" data-num="6" d="M490 240 C 500 190, 540 190, 540 240 Z"></path>
        <path class="zone" data-num="6" d="M610 240 C 600 190, 560 190, 560 240 Z"></path>
        <!-- orejas internas -->
        <path class="zone" data-num="9" d="M505 240 C 510 215, 530 215, 528 240 Z"></path>
        <path class="zone" data-num="9" d="M595 240 C 590 215, 570 215, 572 240 Z"></path>

        <!-- patitas -->
        <ellipse class="zone" data-num="8" cx="520" cy="700" rx="36" ry="22"></ellipse>
        <ellipse class="zone" data-num="8" cx="580" cy="700" rx="36" ry="22"></ellipse>

        <!-- pañuelo / detalle -->
        <path class="zone" data-num="11" d="M360 505c20 10 60 10 80 0-10 20-20 30-40 30s-30-10-40-30z"></path>

        <!-- OJOS y FACIAL (no pintables para evitar tiny clicks) -->
        <circle cx="235" cy="330" r="8" fill="#031226"></circle>
        <circle cx="265" cy="330" r="8" fill="#031226"></circle>
        <circle cx="530" cy="330" r="8" fill="#031226"></circle>
        <circle cx="570" cy="330" r="8" fill="#031226"></circle>

        <!-- NUMERITOS: se colocan con JS para estar exactos sobre zonas -->
      </svg>
    </div>

    <div class="controls" id="controls" aria-hidden="false"></div>

    <div class="bar">
      <button id="hintBtn">Pista</button>
      <button id="resetBtn">Reiniciar</button>
    </div>

    <div id="msg" aria-live="polite"></div>

    <!-- Modal/Reward -->
    <div class="modal" id="modal" role="dialog" aria-modal="true" aria-hidden="true">
      <div class="card">
        <h2 style="margin:6px 0 2px">¡Completado! 🎉</h2>
        <p style="color:var(--muted)">Escanea este QR o abre la playlist</p>
        <div class="qr" id="qrBox"></div>
        <a id="openLink" class="openBtn" target="_blank" rel="noopener">Abrir playlist</a>
      </div>
    </div>

    <div style="height:18px"></div>
    <div style="color:var(--muted);text-align:center;font-size:13px">Consejo: haz zoom con dos dedos (móvil) o Ctrl + rueda (PC) para detalles</div>
    <div style="height:28px"></div>
  </div>
</div>

<script>
/* ========== CONFIG ========== */
const PLAYLIST_URL = "https://open.spotify.com/playlist/6rGxHrCj9w4WLERyNcsbBK?si=rLIOE8kHTDuNQpqXp7lUuw&pi=WxPawjn9RyWAr&nd=1&dlsi=e72b2da00549458d";

/* Número → color + label */
const COLOR_MAP = {
  1:{hex:"#E85D2A", label:"1 — Panda: pelaje rojo"},
  2:{hex:"#F28C34", label:"2 — Panda: franjas cola"},
  3:{hex:"#F5D9A1", label:"3 — Panda: crema"},
  4:{hex:"#FFF2C9", label:"4 — Panda: oreja interna"},
  5:{hex:"#C0C7D1", label:"5 — Mapache: gris claro"},
  6:{hex:"#8B95A5", label:"6 — Mapache: gris medio"},
  7:{hex:"#596273", label:"7 — Mapache: antifaz oscuro"},
  8:{hex:"#1F2430", label:"8 — Patitas/oscuro"},
  9:{hex:"#FFFFFF", label:"9 — Blanco — panza/oreja"},
 10:{hex:"#A0522D", label:"10 — Suelo"},
 11:{hex:"#6BB38E", label:"11 — Pañuelo"},
 12:{hex:"#EFA7D3", label:"12 — Mejillas"}
};

/* ========== UI BUILD ========== */
const controlsEl = document.getElementById('controls');
let selectedNum = null;
Object.entries(COLOR_MAP).forEach(([num, info], idx)=>{
  const ch = document.createElement('div');
  ch.className='chip';
  ch.style.background = info.hex;
  ch.dataset.num = num;
  ch.title = info.label;
  ch.innerHTML = `<div style="font-weight:900;color:rgba(0,0,0,.9)">${num}</div>`;
  ch.addEventListener('click', ()=> {
    document.querySelectorAll('.chip').forEach(c=>c.removeAttribute('data-selected'));
    ch.setAttribute('data-selected','true');
    selectedNum = Number(num);
    setMsg(`Color ${num} seleccionado — ${info.label}`);
  });
  controlsEl.appendChild(ch);
});

/* Mensaje */
const msgEl = document.getElementById('msg');
function setMsg(t, type){
  msgEl.textContent = t || "";
  msgEl.style.color = type === 'bad' ? 'var(--bad)' : (type==='ok' ? 'var(--ok)' : 'var(--muted)');
}

/* find zones and attach numbers text */
const svg = document.getElementById('scene');
const zones = Array.from(svg.querySelectorAll('.zone'));
zones.forEach(z=>{
  // compute center bbox for placing number (approx)
  const bbox = z.getBBox();
  const cx = bbox.x + bbox.width/2;
  const cy = bbox.y + bbox.height/2;
  const n = z.getAttribute('data-num');

  const t = document.createElementNS('http://www.w3.org/2000/svg','text');
  t.classList.add('numText');
  t.setAttribute('x', cx);
  t.setAttribute('y', cy+6);
  t.setAttribute('text-anchor','middle');
  t.textContent = n;
  svg.appendChild(t);

  // initial state:
  z.dataset.filled = "false";
});

/* Interaction: click/tap to paint if selected number matches */
svg.addEventListener('pointerdown', (ev)=>{
  // find target zone element
  const target = ev.target;
  if(!target.classList.contains('zone')) return;
  if(!selectedNum){ setMsg('Selecciona un color antes de pintar.', 'bad'); return; }

  const need = Number(target.getAttribute('data-num'));
  if(need !== selectedNum){
    setMsg('Ese color no va aquí.', 'bad');
    // small visual feedback
    target.animate([{transform:'scale(1)'},{transform:'scale(0.98)'},{transform:'scale(1)'}],{duration:200});
    return;
  }

  // fill zone and mark done
  const color = COLOR_MAP[need].hex;
  target.style.fill = color;
  target.classList.add('filled');
  target.dataset.filled = "true";

  // remove the number text overlay for that zone (closest by coords)
  const bbox = target.getBBox();
  const cx = bbox.x + bbox.width/2;
  const cy = bbox.y + bbox.height/2;
  const texts = Array.from(svg.querySelectorAll('.numText'));
  const found = texts.find(t => Math.abs(t.getAttribute('x') - cx) < 6 && Math.abs(t.getAttribute('y') - (cy+6)) < 8);
  if(found) found.remove();

  setMsg('Perfecto ✔', 'ok');
  checkComplete();
});

/* HINT button: find one remaining zone for currently selected number and animate it */
document.getElementById('hintBtn').addEventListener('click', ()=>{
  if(!selectedNum){ setMsg('Selecciona un color para recibir una pista.', 'bad'); return; }
  const candidate = zones.find(z => z.dataset.filled === "false" && Number(z.dataset.num) === selectedNum);
  if(!candidate){ setMsg('No quedan zonas con ese número. Cambia de color.', 'ok'); return; }
  // animate stroke
  candidate.animate([{strokeWidth:2},{strokeWidth:8},{strokeWidth:2}],{duration:700});
  setMsg(`Pista: fíjate la zona con el número ${selectedNum}.`, 'ok');
});

/* RESET */
document.getElementById('resetBtn').addEventListener('click', ()=>{
  zones.forEach(z=>{
    z.style.fill = "#fff";
    z.classList.remove('filled');
    z.dataset.filled = "false";
  });
  // restore numbers
  const existingNums = Array.from(svg.querySelectorAll('.numText'));
  existingNums.forEach(n=>n.remove());
  zones.forEach(z=> {
    const bbox = z.getBBox();
    const cx = bbox.x + bbox.width/2;
    const cy = bbox.y + bbox.height/2;
    const n = z.getAttribute('data-num');
    const t = document.createElementNS('http://www.w3.org/2000/svg','text');
    t.classList.add('numText');
    t.setAttribute('x', cx);
    t.setAttribute('y', cy+6);
    t.setAttribute('text-anchor','middle');
    t.textContent = n;
    svg.appendChild(t);
  });
  setMsg('Lienzo reiniciado. Elige un color para empezar.');
  document.getElementById('modal').classList.remove('show');
  document.getElementById('modal').setAttribute('aria-hidden','true');
});

/* Check completion */
function checkComplete(){
  const done = zones.every(z => z.dataset.filled === "true");
  if(done){
    setMsg('¡Has completado el dibujo! 🎉', 'ok');
    // show modal with QR
    const modal = document.getElementById('modal');
    const qrBox = document.getElementById('qrBox');
    const openLink = document.getElementById('openLink');
    openLink.href = PLAYLIST_URL;
    // generate QR using Google Chart API
    const qrUrl = `https://chart.googleapis.com/chart?cht=qr&chs=400x400&chl=${encodeURIComponent(PLAYLIST_URL)}&chld=L|0`;
    qrBox.innerHTML = `<img src="${qrUrl}" alt="QR" style="width:100%;height:100%;object-fit:contain;border-radius:8px"/>`;
    modal.classList.add('show');
    modal.setAttribute('aria-hidden','false');
    // scroll to top the modal on small screens
    setTimeout(()=>window.scrollTo({top:0,behavior:'smooth'}),50);
  }
}

/* Close modal on overlay click */
document.getElementById('modal').addEventListener('click',(e)=>{
  if(e.target === e.currentTarget){
    e.currentTarget.classList.remove('show');
    e.currentTarget.setAttribute('aria-hidden','true');
  }
});

/* inicial */
setMsg('Elige un color en la paleta para comenzar.');
</script>
</body>
</html>
