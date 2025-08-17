<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Pinta por números — Panda rojo & Mapache (detallado)</title>
<style>
  :root{
    --bg:#071226; --panel:#07182a; --card:#0b2133; --text:#e8f1fb; --muted:#97adca;
    --accent:#f6b26b; --ok:#3ee6a0; --bad:#ff7b7b;
  }
  *{box-sizing:border-box}
  body{margin:0;background:linear-gradient(180deg,#061022 0%,#071428 100%);color:var(--text);font-family:Inter,system-ui, -apple-system, "Segoe UI", Roboto, Arial}
  header{padding:18px 12px;text-align:center}
  h1{margin:0;font-size:clamp(18px,3.8vw,30px)}
  p.lead{margin:6px 0;color:var(--muted);max-width:880px;margin-left:auto;margin-right:auto}
  .wrap{max-width:1080px;margin:18px auto;padding:0 14px}
  .board{background:var(--panel);border-radius:14px;padding:14px;box-shadow:0 10px 40px rgba(2,6,23,.6)}
  .svgwrap{max-width:980px;margin:0 auto;touch-action:none}
  svg{width:100%;height:auto;display:block}
  .controls{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px}
  .chip{width:46px;height:46px;border-radius:50%;display:grid;place-items:center;font-weight:800;color:#041226;border:2px solid rgba(255,255,255,.06);cursor:pointer}
  .chip[data-selected="true"]{outline:3px solid var(--accent);box-shadow:0 8px 26px rgba(0,0,0,.6)}
  .legend{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:8px;margin-top:12px}
  .legendItem{display:flex;gap:10px;align-items:center;padding:8px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,.02), transparent)}
  .sw{width:22px;height:22px;border-radius:50%;border:1px solid rgba(0,0,0,.15)}
  .bar{display:flex;gap:8px;justify-content:center;margin-top:12px}
  button{background:#0f2540;border:1px solid #1e3a5a;color:var(--text);padding:10px 12px;border-radius:10px;cursor:pointer;font-weight:700}
  button:hover{filter:brightness(1.06)}
  #msg{min-height:28px;text-align:center;margin:12px 0;color:var(--muted)}
  .modal{position:fixed;inset:0;display:grid;place-items:center;background:rgba(4,6,12,.75);z-index:60;opacity:0;pointer-events:none;transition:opacity .18s}
  .modal.show{opacity:1;pointer-events:auto}
  .card{background:linear-gradient(180deg,#071428,#061226);border-radius:12px;padding:18px;border:1px solid rgba(255,255,255,.06);max-width:460px;text-align:center}
  .qr{width:260px;height:260px;margin:10px auto;background:#fff;padding:10px;border-radius:12px}
  a.openBtn{display:inline-block;margin-top:10px;padding:10px 14px;border-radius:12px;background:var(--accent);color:#04122b;text-decoration:none;font-weight:800}
  @media (max-width:760px){.chip{width:40px;height:40px}.qr{width:200px;height:200px}}
  /* SVG zone baseline styling */
  .zone{fill:#fff;stroke:#081226;stroke-width:2;cursor:pointer}
  .zone.filled{stroke:#031018}
  .numText{font-weight:800;fill:#081726;stroke:#fff;stroke-width:3px;font-size:12px;pointer-events:none}
</style>
</head>
<body>
<header>
  <h1>Pinta por números — Panda Rojo & Mapache</h1>
  <p class="lead">Elige el número/color correcto y toca la zona para colorearla. Cuando termines aparecerá la sorpresa: la playlist.</p>
</header>

<div class="wrap">
  <div class="board" role="application" aria-label="Pinta por números">
    <div class="svgwrap" id="svgwrap">
      <!-- SVG 1200x900 para mayor detalle (escalará responsivo) -->
      <svg id="scene" viewBox="0 0 1200 900" role="img" aria-labelledby="title desc">
        <title id="title">Panda rojo y mapache — pintar por números (detallado)</title>
        <desc id="desc">Ilustración vectorial dividida en muchas zonas numeradas para colorear</desc>

        <!-- fondo transparente -->
        <rect x="0" y="0" width="1200" height="900" fill="transparent"></rect>

        <!-- --------- SUELO (10) --------- -->
        <rect class="zone" data-num="10" x="40" y="820" width="1120" height="60"></rect>

        <!-- ================= PANDA ROJO (IZQ) ================= -->
        <!-- cola con franjas (zonas 21,22,23,...) -->
        <g id="panda-tail-group">
          <ellipse class="zone" data-num="21" cx="310" cy="680" rx="110" ry="54"></ellipse>
          <path class="zone" data-num="22" d="M220,660 q80,50 160,40 q-40,20 -90,30 q-100,-10 -70,-70z"></path>
          <rect class="zone" data-num="23" x="220" y="640" width="36" height="24" rx="8"></rect>
          <rect class="zone" data-num="23" x="260" y="628" width="36" height="24" rx="8" transform="rotate(-10 278 640)"></rect>
        </g>

        <!-- cuerpo principal -->
        <ellipse class="zone" data-num="1" cx="370" cy="520" rx="165" ry="210"></ellipse>
        <!-- vientre -->
        <ellipse class="zone" data-num="3" cx="370" cy="560" rx="100" ry="135"></ellipse>

        <!-- brazos -->
        <path class="zone" data-num="1" d="M450 480 q40 40 28 90 q-20 30 -56 18 q-20 -30 -12 -94z"></path>
        <path class="zone" data-num="1" d="M290 480 q-40 40 -28 90 q20 30 56 18 q20 -30 12 -94z"></path>

        <!-- manos y dedos (cada dedo separado para tactilidad) -->
        <g id="panda-hand-left">
          <ellipse class="zone" data-num="12" cx="292" cy="540" rx="34" ry="26"></ellipse>
          <ellipse class="zone" data-num="12" cx="320" cy="540" rx="18" ry="16"></ellipse>
        </g>
        <g id="panda-hand-right">
          <ellipse class="zone" data-num="12" cx="428" cy="540" rx="34" ry="26"></ellipse>
          <ellipse class="zone" data-num="12" cx="398" cy="540" rx="18" ry="16"></ellipse>
        </g>

        <!-- cabeza -->
        <ellipse class="zone" data-num="1" cx="370" cy="320" rx="120" ry="118"></ellipse>
        <!-- cara interna (máscara clara) -->
        <path class="zone" data-num="3" d="M300 320 q70 -70 140 0 q-70 60 -140 0z" transform="translate(0,8)"></path>

        <!-- orejas externas -->
        <path class="zone" data-num="1" d="M290 220 q-34 -40 -70 -10 q40 40 70 10z"></path>
        <path class="zone" data-num="1" d="M450 220 q34 -40 70 -10 q-40 40 -70 10z"></path>
        <!-- orejas internas -->
        <path class="zone" data-num="4" d="M300 230 q-18 -20 -32 -8 q16 20 32 8z"></path>
        <path class="zone" data-num="4" d="M440 230 q18 -20 32 -8 q-16 20 -32 8z"></path>

        <!-- mejillas -->
        <circle class="zone" data-num="12" cx="340" cy="350" r="18"></circle>
        <circle class="zone" data-num="12" cx="400" cy="350" r="18"></circle>

        <!-- ojos y nariz (no pintables) -->
        <circle cx="355" cy="325" r="10" fill="#031022"></circle>
        <circle cx="385" cy="325" r="10" fill="#031022"></circle>
        <ellipse cx="370" cy="360" rx="12" ry="8" fill="#031022"></ellipse>

        <!-- detalles faciales - franjas -->
        <path class="zone" data-num="2" d="M310 300 q40 -30 60 -30 q-20 12 -45 38z"></path>
        <path class="zone" data-num="2" d="M430 300 q-40 -30 -60 -30 q20 12 45 38z"></path>

        <!-- patas -->
        <ellipse class="zone" data-num="8" cx="310" cy="770" rx="58" ry="36"></ellipse>
        <ellipse class="zone" data-num="8" cx="430" cy="770" rx="58" ry="36"></ellipse>

        <!-- --------- DETALLES PANDA (pequeñas zonas para hacer creíble) --------- -->
        <path class="zone" data-num="2" d="M335 290 q10 6 20 8 q-8 4 -20 -8z"></path>
        <path class="zone" data-num="2" d="M405 290 q-10 6 -20 8 q8 4 20 -8z"></path>

        <!-- bufanda o pañuelo -->
        <path class="zone" data-num="11" d="M360 440 q20 18 80 10 q-10 34 -38 36 q-42 -8 -42 -56z"></path>

        <!-- ================= MAPACHE (DERECHA) ================= -->
        <!-- cola con franjas (zonas 31..34) -->
        <g id="raccoon-tail-group">
          <ellipse class="zone" data-num="31" cx="930" cy="680" rx="120" ry="56"></ellipse>
          <path class="zone" data-num="32" d="M830,660 q90,70 190,40 q-30,20 -100,36 q-80,-6 -90,-76z"></path>
          <rect class="zone" data-num="33" x="840" y="620" width="44" height="30" rx="12"></rect>
          <rect class="zone" data-num="33" x="885" y="606" width="44" height="30" rx="12"></rect>
        </g>

        <!-- cuerpo -->
        <ellipse class="zone" data-num="5" cx="790" cy="520" rx="165" ry="210"></ellipse>
        <!-- panza -->
        <ellipse class="zone" data-num="9" cx="790" cy="560" rx="100" ry="135"></ellipse>

        <!-- brazos -->
        <path class="zone" data-num="6" d="M715 480 q-40 40 -30 94 q12 26 56 12 q12 -30 -12 -96z"></path>
        <path class="zone" data-num="6" d="M865 480 q40 40 30 94 q-12 26 -56 12 q-12 -30 12 -96z"></path>

        <!-- manos (tomando la mano del panda, zona central) -->
        <ellipse class="zone" data-num="12" cx="600" cy="540" rx="28" ry="22"></ellipse>
        <ellipse class="zone" data-num="12" cx="625" cy="540" rx="28" ry="22"></ellipse>

        <!-- cabeza -->
        <ellipse class="zone" data-num="5" cx="790" cy="320" rx="120" ry="118"></ellipse>

        <!-- antifaz oscuro (varias piezas para dar detalle) -->
        <path class="zone" data-num="7" d="M700 300 q90 -66 200 0 q-90 60 -200 0z" transform="translate(0,6)"></path>
        <path class="zone" data-num="7" d="M720 320 q60 -20 160 -20 q-60 24 -160 20z"></path>

        <!-- orejas -->
        <path class="zone" data-num="6" d="M725 220 q-34 -40 -70 -10 q40 40 70 10z"></path>
        <path class="zone" data-num="6" d="M855 220 q34 -40 70 -10 q-40 40 -70 10z"></path>
        <!-- orejas internas -->
        <path class="zone" data-num="9" d="M735 230 q-18 -20 -32 -8 q16 20 32 8z"></path>
        <path class="zone" data-num="9" d="M845 230 q18 -20 32 -8 q-16 20 -32 8z"></path>

        <!-- mejillas sutiles -->
        <circle class="zone" data-num="12" cx="760" cy="350" r="14"></circle>
        <circle class="zone" data-num="12" cx="820" cy="350" r="14"></circle>

        <!-- patas -->
        <ellipse class="zone" data-num="8" cx="740" cy="770" rx="58" ry="36"></ellipse>
        <ellipse class="zone" data-num="8" cx="840" cy="770" rx="58" ry="36"></ellipse>

        <!-- franjas en cola (pequeñas rayas) -->
        <path class="zone" data-num="33" d="M900 665 q-60 40 -120 30 q30 10 120 0z"></path>
        <path class="zone" data-num="33" d="M850 650 q-50 30 -100 30 q20 8 100 0z"></path>

        <!-- detalles faciales: máscara menor y hocico  -->
        <path class="zone" data-num="7" d="M760 310 q30 18 66 20 q-34 10 -66 -20z"></path>
        <ellipse class="zone" data-num="9" cx="790" cy="360" rx="12" ry="8"></ellipse>

        <!-- ---- manos centrales: corazoncito y unión ---- -->
        <path class="zone" data-num="12" d="M565 510 q30 -20 70 -20 q40 0 70 20 q-30 40 -70 50 q-50 -10 -70 -50z"></path>

        <!-- algunos adornos (peques) -->
        <circle class="zone" data-num="11" cx="430" cy="400" r="10"></circle>
        <circle class="zone" data-num="11" cx="730" cy="400" r="10"></circle>

        <!-- OJOS (no pintables) -->
        <circle cx="355" cy="325" r="10" fill="#031022"></circle>
        <circle cx="385" cy="325" r="10" fill="#031022"></circle>
        <circle cx="760" cy="320" r="10" fill="#031022"></circle>
        <circle cx="820" cy="320" r="10" fill="#031022"></circle>

        <!-- ---------- FINAL: Números ubicados por JS (no añadidos aquí para evitar superposición automática) ---------- -->

      </svg>
    </div>

    <!-- controles -->
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

    <div style="height:10px"></div>
    <div style="color:var(--muted);text-align:center;font-size:13px">Consejo: haz zoom con dos dedos (móvil) o Ctrl + rueda (PC) para detalles</div>
    <div style="height:18px"></div>
  </div>
</div>

<script>
/* CONFIG */
const PLAYLIST_URL = "https://open.spotify.com/playlist/6rGxHrCj9w4WLERyNcsbBK?si=rLIOE8kHTDuNQpqXp7lUuw&pi=WxPawjn9RyWAr&nd=1&dlsi=e72b2da00549458d";

/* MAPA NÚMERO → color y etiqueta (ampliaremos según zonas) */
const COLOR_MAP = {
  1:{hex:"#E85D2A", label:"Pelaje panda (rojo)"},
  2:{hex:"#D95526", label:"Marcas panda (oscuro)"},
  3:{hex:"#F5D9A1", label:"Panza/mascara crema"},
  4:{hex:"#FFEFCB", label:"Oreja interna (clara)"},
  5:{hex:"#C0C7D1", label:"Mapache base gris"},
  6:{hex:"#9AA3B2", label:"Mapache medio"},
  7:{hex:"#5B6470", label:"Mapache antifaz oscuro"},
  8:{hex:"#1F2430", label:"Sombras/patitas oscuras"},
  9:{hex:"#FFFFFF", label:"Blanco (panza/oreja)"},
 10:{hex:"#A0522D", label:"Suelo / base"},
 11:{hex:"#6BB38E", label:"Accentos / bufanda"},
 12:{hex:"#EFA7D3", label:"Mejillas / detalles suaves"},
 21:{hex:"#C14E28", label:"Cola panda - banda 1"},
 22:{hex:"#B44424", label:"Cola panda - banda 2"},
 23:{hex:"#9E3A20", label:"Cola panda - remates"},
 31:{hex:"#ACB3BD", label:"Cola mapache - banda 1"},
 32:{hex:"#9AA3B2", label:"Cola mapache - banda 2"},
 33:{hex:"#788189", label:"Franjas pequeñas cola mapache"},
};

/* Construye paleta en UI */
const controlsEl = document.getElementById('controls');
let selectedNum = null;
Object.keys(COLOR_MAP).sort((a,b)=>Number(a)-Number(b)).forEach(key=>{
  const info = COLOR_MAP[key];
  const ch = document.createElement('div');
  ch.className = 'chip';
  ch.style.background = info.hex;
  ch.dataset.num = key;
  ch.title = `${key} — ${info.label}`;
  ch.innerHTML = `<div style="font-weight:900;color:rgba(0,0,0,.85)">${key}</div>`;
  ch.addEventListener('click', ()=> {
    document.querySelectorAll('.chip').forEach(c=>c.removeAttribute('data-selected'));
    ch.setAttribute('data-selected','true');
    selectedNum = Number(key);
    setMsg(`Color ${key} seleccionado — ${info.label}`, 'ok');
  });
  controlsEl.appendChild(ch);
});

/* Mensajes */
const msgEl = document.getElementById('msg');
function setMsg(t, type){
  msgEl.textContent = t || "";
  msgEl.style.color = type === 'bad' ? 'var(--bad)' : (type === 'ok' ? 'var(--ok)' : 'var(--muted)');
}

/* Selecciona zonas, coloca números en centros no superpuestos manualmente */
const svg = document.getElementById('scene');
const zones = Array.from(svg.querySelectorAll('.zone'));

/* Para evitar superposición de números, calculo un conjunto de coordenadas "seguras" manuales.
   Aquí voy a mapear zona -> textoPosition (x,y). Si alguna zona necesita ajuste lo cambias aquí. */
const NUM_POS = {
  // panda: usamos coordenadas aproximadas dentro del viewport 1200x900
  "1":[370,315],
  "2":[335,265],
  "3":[370,560],
  "4":[300,235],
  "5":[790,315],
  "6":[765,268],
  "7":[760,325],
  "8":[720,745],
  "9":[790,560],
  "10":[600,850],
  "11":[370,420],
  "12":[595,520],
  "21":[300,640],
  "22":[260,640],
  "23":[230,620],
  "31":[930,640],
  "32":[880,640],
  "33":[870,610]
};

/* Añadir textos (números) en puntos definidos para que no se superpongan */
function placeNumbers(){
  // Primero borrar prévios
  Array.from(svg.querySelectorAll('.numText')).forEach(t=>t.remove());

  zones.forEach(z=>{
    const num = z.getAttribute('data-num');
    const pos = NUM_POS[num];
    // si no hay posición definida, calculo centro bbox + pequeño desplazamiento para evitar superposiciones
    let x,y;
    if(pos){
      x = pos[0]; y = pos[1];
    } else {
      const bb = z.getBBox();
      x = bb.x + bb.width/2;
      y = bb.y + bb.height/2 + 6;
    }
    // crear texto
    const t = document.createElementNS('http://www.w3.org/2000/svg','text');
    t.classList.add('numText');
    t.setAttribute('x', x);
    t.setAttribute('y', y);
    t.setAttribute('text-anchor','middle');
    t.textContent = num;
    svg.appendChild(t);
  });
}

/* Inicial colocar números */
placeNumbers();

/* Interacción pintar: solo si selectedNum coincide con data-num */
svg.addEventListener('pointerdown', (ev)=>{
  const target = ev.target;
  if(!target.classList.contains('zone')) return;
  if(!selectedNum){ setMsg('Selecciona un color antes de pintar.', 'bad'); return; }

  const need = Number(target.getAttribute('data-num'));
  if(need !== selectedNum){
    setMsg('Ese color no va aquí.', 'bad');
    target.animate([{transform:'scale(1)'},{transform:'scale(.98)'},{transform:'scale(1)'}],{duration:180});
    return;
  }

  // pintar
  const color = COLOR_MAP[need].hex;
  target.style.fill = color;
  target.classList.add('filled');
  target.dataset.filled = "true";

  // borrar numerito cercano (búsqueda por proximidad)
  const bb = target.getBBox();
  const cx = bb.x + bb.width/2;
  const cy = bb.y + bb.height/2 + 6;
  const texts = Array.from(svg.querySelectorAll('.numText'));
  const tol = 20;
  let found = null;
  for(const t of texts){
    const tx = Number(t.getAttribute('x'));
    const ty = Number(t.getAttribute('y'));
    if(Math.abs(tx - cx) < tol && Math.abs(ty - cy) < tol){
      found = t; break;
    }
  }
  if(found) found.remove();

  setMsg('Perfecto ✓', 'ok');
  checkComplete();
});

/* Pista: resalta una zona restante del número seleccionado */
document.getElementById('hintBtn').addEventListener('click', ()=>{
  if(!selectedNum){ setMsg('Selecciona un color para recibir una pista.', 'bad'); return; }
  const candidate = zones.find(z => z.dataset.filled !== "true" && Number(z.dataset.num) === selectedNum);
  if(!candidate){ setMsg('No quedan zonas con ese número. Cambia de color.', 'ok'); return; }
  candidate.animate([{filter:'brightness(1)'},{filter:'brightness(2.4)'},{filter:'brightness(1)'}],{duration:700});
  setMsg(`Pista: fíjate la zona con el número ${selectedNum}.`, 'ok');
});

/* Reset */
document.getElementById('resetBtn').addEventListener('click', ()=>{
  zones.forEach(z=>{
    z.style.fill = "#fff";
    z.classList.remove('filled');
    z.dataset.filled = "false";
  });
  placeNumbers();
  setMsg('Lienzo reiniciado. Elige un color para empezar.');
  document.getElementById('modal').classList.remove('show');
  document.getElementById('modal').setAttribute('aria-hidden','true');
});

/* Check si todas las zonas están pintadas */
function checkComplete(){
  const notDone = zones.filter(z => z.dataset.filled !== "true");
  if(notDone.length === 0){
    setMsg('¡Has completado el dibujo! 🎉', 'ok');
    // mostrar modal con QR
    const modal = document.getElementById('modal');
    const qrBox = document.getElementById('qrBox');
    const openLink = document.getElementById('openLink');
    openLink.href = PLAYLIST_URL;
    const qrUrl = `https://chart.googleapis.com/chart?cht=qr&chs=500x500&chl=${encodeURIComponent(PLAYLIST_URL)}&chld=L|0`;
    qrBox.innerHTML = `<img src="${qrUrl}" alt="QR" style="width:100%;height:100%;object-fit:contain;border-radius:8px"/>`;
    modal.classList.add('show');
    modal.setAttribute('aria-hidden','false');
    setTimeout(()=>window.scrollTo({top:0,behavior:'smooth'}),50);
  } else {
    setMsg(`${zones.length - notDone.length} / ${zones.length} pintadas`, 'ok');
  }
}

/* Cerrar modal con clic en overlay */
document.getElementById('modal').addEventListener('click',(e)=>{
  if(e.target === e.currentTarget){
    e.currentTarget.classList.remove('show');
    e.currentTarget.setAttribute('aria-hidden','true');
  }
});

/* Mensaje inicial */
setMsg('Elige un color en la paleta para comenzar.');

/* mejora: si la ventana cambia tamaño, recolocar numeritos (por si alguna zona quedó movida) */
window.addEventListener('resize', ()=> { placeNumbers(); });

</script>
</body>
</html>
