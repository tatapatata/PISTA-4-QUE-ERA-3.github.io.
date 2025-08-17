<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <title>Pinta por números — Panda Rojo & Mapache</title>
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <style>
    :root{
      --bg:#0e0f12;
      --panel:#151820;
      --ink:#e6e6e6;
      --muted:#9aa4b2;
      --brand:#6e8efb;
      --brand2:#a777e3;
      --ok:#30d158;
      --warn:#ff9f0a;
      --err:#ff453a;
    }
    *{box-sizing:border-box}
    body{
      margin:0; background:linear-gradient(135deg,var(--bg),#0b0c10);
      color:var(--ink); font-family:Inter,system-ui,Segoe UI,Roboto,Helvetica,Arial,sans-serif;
      -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
    }
    .wrap{
      max-width:1100px; margin-inline:auto; padding:24px; display:grid; gap:16px;
      grid-template-columns: 1fr; 
    }
    @media (min-width: 980px){
      .wrap{ grid-template-columns: 1.1fr .9fr; align-items:start; }
    }
    .card{
      background:linear-gradient(180deg,rgba(255,255,255,.02),rgba(255,255,255,.01));
      border:1px solid rgba(255,255,255,.08);
      border-radius:16px; box-shadow:0 10px 30px rgba(0,0,0,.25);
      padding:16px;
    }
    .title{
      font-weight:700; letter-spacing:.2px; margin:0 0 8px 0; font-size:20px;
    }
    .sub{ color:var(--muted); font-size:14px; margin-top:4px }
    .board{
      display:flex; align-items:center; justify-content:center;
      background:#0d0f15; border-radius:14px; border:1px solid rgba(255,255,255,.06);
      min-height: 420px; padding:10px; position:relative; overflow:hidden;
    }
    .svgHost{
      width:100%; max-width:900px; aspect-ratio:1/1;
      background:radial-gradient(100% 100% at 30% 20%, #10131b 0%, #0c0f15 100%);
      border-radius:12px; border:1px solid rgba(255,255,255,.06);
      display:grid; place-items:center; position:relative;
      touch-action: manipulation; /* para móvil */
    }
    /* Paleta */
    .palette{
      display:flex; flex-wrap:wrap; gap:10px; padding:10px;
    }
    .swatch{
      display:flex; align-items:center; gap:8px; padding:8px 10px;
      border-radius:12px; cursor:pointer; user-select:none;
      border:1px solid rgba(255,255,255,.08);
      background:linear-gradient(180deg,rgba(255,255,255,.03),rgba(255,255,255,.01));
      transition:transform .08s ease, box-shadow .2s ease, border-color .2s ease;
      min-width: 82px;
    }
    .swatch[aria-current="true"]{
      outline:0; border-color:var(--brand);
      box-shadow:0 0 0 3px rgba(110,142,251,.25);
      transform: translateY(-1px);
    }
    .swatch-chip{
      inline-size:22px; block-size:22px; border-radius:6px; border:1px solid rgba(0,0,0,.35);
      box-shadow: inset 0 0 0 1px rgba(255,255,255,.15);
    }
    .swatch-lab{ font-size:13px }
    .legend{
      display:flex; align-items:center; gap:8px; flex-wrap:wrap;
      color:var(--muted); font-size:13px; padding:6px 10px 2px;
    }
    .progress{
      margin-top:10px; background:#0d1118; border-radius:10px; border:1px solid rgba(255,255,255,.08);
      height:12px; position:relative; overflow:hidden;
    }
    .bar{
      position:absolute; inset:0 auto 0 0; width:0%; background:linear-gradient(90deg,var(--brand),var(--brand2));
      border-right:1px solid rgba(255,255,255,.3);
      box-shadow: 0 4px 16px rgba(110,142,251,.45);
    }
    .pct{ font-size:12px; color:var(--muted); margin-top:6px; text-align:right }

    /* Estado y ayudas */
    .hint{ font-size:13px; color:var(--muted); margin-top:6px; }
    .toast{
      position:fixed; left:50%; translate:-50% 0; bottom:22px;
      background:#121723; border:1px solid rgba(255,255,255,.12); color:var(--ink);
      padding:10px 14px; border-radius:12px; box-shadow:0 12px 32px rgba(0,0,0,.35);
      display:none; z-index:50;
    }
    .toast.show{ display:block; animation: pop .18s ease-out }
    @keyframes pop{ from{ transform: translate(-50%,4px); opacity:.0 } to{ transform: translate(-50%,0); opacity:1 } }

    /* Números pintables generados */
    .zone-num{
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace;
      fill: #dfe6f0; font-size: 14px; pointer-events:none;
      paint-order: stroke; stroke: #0d0f15; stroke-width: 3px; stroke-linejoin: round;
      opacity: .9;
    }

    /* Modal final */
    .modal{
      position: fixed; inset:0; display:none; place-items:center; padding:20px; z-index:60;
      background: rgba(0,0,0,.55);
    }
    .modal-inner{
      width:min(720px,96vw);
      background:linear-gradient(180deg,#111522,#0f1320);
      border:1px solid rgba(255,255,255,.12);
      border-radius:18px; padding:18px;
      box-shadow:0 20px 50px rgba(0,0,0,.45);
      text-align:center;
    }
    .modal h2{ margin:6px 0 8px; font-size:22px }
    .modal p{ margin:0; color:var(--muted) }
    .qr{
      margin:16px auto 8px; width:min(280px,65vw); border-radius:12px;
      border:1px solid rgba(255,255,255,.1); background:#0a0d14; padding:8px;
    }
    .btnRow{ display:flex; gap:10px; justify-content:center; margin-top:10px; flex-wrap:wrap }
    .btn{
      background:linear-gradient(90deg,var(--brand),var(--brand2));
      color:white; border:0; border-radius:12px; padding:10px 14px; cursor:pointer; font-weight:600;
      box-shadow:0 10px 24px rgba(110,142,251,.35);
    }
    .btn.alt{
      background:transparent; color:var(--ink); border:1px solid rgba(255,255,255,.16)
    }
    .tiny{
      font-size:12px; color:var(--muted); margin-top:6px;
    }

    /* Accesibilidad/estado */
    .shake{ animation:shake .2s linear 1 }
    @keyframes shake{
      10%, 90% { transform: translateX(-1px) }
      20%, 80% { transform: translateX(2px) }
      30%, 50%, 70% { transform: translateX(-4px) }
      40%, 60% { transform: translateX(4px) }
    }
  </style>
</head>
<body>
  <div class="wrap">
    <section class="card">
      <h1 class="title">Panda rojo & Mapache — pinta por números</h1>
      <div class="sub">Elige un número en la paleta y pinta las zonas con el mismo número. Cuando termines, se desbloqueará una sorpresa 🎁</div>
      <div class="board">
        <div id="svgHost" class="svgHost" aria-live="polite">
          <div class="hint">Cargando dibujo…</div>
        </div>
      </div>
      <div class="legend">Paleta activa:</div>
      <div id="palette" class="palette" role="listbox" aria-label="Paleta de colores"></div>
      <div class="progress" aria-hidden="true"><div id="bar" class="bar"></div></div>
      <div id="pct" class="pct">0% completado</div>
      <div class="hint">Tip: puedes pellizcar para hacer zoom (móvil) o Ctrl/Cmd + rueda (PC) en tu navegador.</div>
    </section>

    <aside class="card">
      <h2 class="title">Instrucciones</h2>
      <ol style="margin:0 0 6px 16px; line-height:1.5">
        <li>Toca / haz click en un color de la paleta.</li>
        <li>Luego toca una zona del dibujo con el mismo número.</li>
        <li>Repite hasta completar todas las zonas.</li>
      </ol>
      <p class="sub">Si eliges un número distinto, el lienzo te avisará. Nada se perderá.</p>

      <h3 class="title" style="margin-top:16px">Leyenda de colores</h3>
      <div class="sub">Los números dependen del SVG. Esta app detecta y muestra solo los necesarios.</div>
      <ul id="legendList" style="margin:8px 0 0 14px; line-height:1.4"></ul>

      <div class="tiny">¿Problemas para ver los números? Haz zoom en el navegador o gira tu teléfono a horizontal.</div>
    </aside>
  </div>

  <div id="toast" class="toast" role="status" aria-live="polite"></div>

  <!-- Modal final -->
  <div id="modal" class="modal" role="dialog" aria-modal="true" aria-label="Sorpresa desbloqueada">
    <div class="modal-inner">
      <h2>¡Completaste el dibujo! 🧩</h2>
      <p>Escanea el QR o toca el botón para abrir la playlist.</p>
      <img class="qr" src="playlist_qr.png" alt="QR de la playlist" onerror="this.style.display='none'">
      <div class="btnRow">
        <a class="btn" href="https://open.spotify.com/playlist/6rGxHrCj9w4WLERyNcsbBK?si=rLIOE8kHTDuNQpqXp7lUuw" target="_blank" rel="noopener">Abrir playlist</a>
        <button class="btn alt" onclick="closeModal()">Cerrar</button>
      </div>
      <div class="tiny">Si el QR no se ve, usa el botón “Abrir playlist”.</div>
    </div>
  </div>

  <script>
    // === Config ===
    const SVG_FILE = 'panda_mapache_colorear.svg'; // Debe estar junto a este index.html
    // Mapa (número -> color). Puedes ajustar tonos si quieres.
    const COLOR_MAP = {
      1:'#e63946', 2:'#ff7f50', 3:'#f1a208', 4:'#ffd166', 5:'#06d6a0',
      6:'#118ab2', 7:'#8a5cf6', 8:'#c77dff', 9:'#ef476f', 10:'#73d2de',
      11:'#2a9d8f', 12:'#e76f51', 13:'#264653', 14:'#4a5568', 15:'#f2f2f2',
      16:'#a3a3a3', 17:'#865439', 18:'#d4a373', 19:'#ffb4a2', 20:'#b56576'
    };

    let currentNum = null;
    let zones = []; // {el, num, filled}
    let totalZones = 0;
    let filledCount = 0;

    const host = document.getElementById('svgHost');
    const palette = document.getElementById('palette');
    const bar = document.getElementById('bar');
    const pct = document.getElementById('pct');
    const toast = document.getElementById('toast');
    const legendList = document.getElementById('legendList');

    // Util: toast
    function say(msg){
      toast.textContent = msg;
      toast.classList.add('show');
      clearTimeout(say._t);
      say._t = setTimeout(()=>toast.classList.remove('show'), 1500);
    }

    // Modal
    function openModal(){ document.getElementById('modal').style.display='grid'; }
    function closeModal(){ document.getElementById('modal').style.display='none'; }
    window.closeModal = closeModal;

    // Carga SVG y lo inyecta
    fetch(SVG_FILE).then(r=>r.text()).then(txt=>{
      host.innerHTML = txt;
      const svg = host.querySelector('svg');
      if(!svg){
        host.innerHTML = '<div class="hint">No se pudo cargar el SVG. Verifica el nombre del archivo.</div>';
        return;
      }
      // Ajuste responsivo
      svg.style.width = '95%';
      svg.style.height = '95%';
      svg.setAttribute('preserveAspectRatio','xMidYMid meet');
      // Busca zonas con atributo data-num (asegura que tu SVG use data-num="N" en cada zona pintable)
      const zoneNodes = svg.querySelectorAll('[data-num]');
      if(!zoneNodes.length){
        host.insertAdjacentHTML('beforeend','<div class="hint">No se encontraron zonas con <code>data-num</code> en el SVG.</div>');
      }

      // Construye set de números presentes
      const presentNums = new Set();
      zoneNodes.forEach(el=>{
        const n = Number(el.getAttribute('data-num'));
        if(Number.isFinite(n)) presentNums.add(n);
      });

      // Paleta dinámica solo con números presentes
      const numsSorted = [...presentNums].sort((a,b)=>a-b);
      numsSorted.forEach(n=>{
        const color = COLOR_MAP[n] || '#888';
        const sw = document.createElement('button');
        sw.className = 'swatch';
        sw.setAttribute('role','option');
        sw.dataset.num = String(n);
        sw.innerHTML = `
          <span class="swatch-chip" style="background:${color}"></span>
          <span class="swatch-lab">N° ${n}</span>
        `;
        sw.addEventListener('click', ()=>{
          [...palette.children].forEach(c=>c.removeAttribute('aria-current'));
          sw.setAttribute('aria-current','true');
          currentNum = n;
          say('Número activo: ' + n);
        });
        palette.appendChild(sw);
      });

      // Leyenda / lista
      legendList.innerHTML = numsSorted.map(n=>{
        const c = COLOR_MAP[n] || '#888';
        return `<li> <strong>N° ${n}</strong> — <span style="color:${c}">${c}</span></li>`;
      }).join('');

      // Prepara cada zona
      zones = [];
      zoneNodes.forEach(el=>{
        const num = Number(el.getAttribute('data-num'));
        zones.push({el, num, filled:false});
        // Estilo inicial
        el.style.fill = 'transparent';
        el.style.cursor = 'pointer';
        el.style.stroke = 'rgba(255,255,255,.35)';
        el.style.strokeWidth = '0.6';
        el.style.transition = 'fill .08s ease';
        // Click para pintar
        el.addEventListener('click', (ev)=>{
          ev.preventDefault();
          if(currentNum == null){ say('Elige un número en la paleta.'); host.classList.add('shake'); setTimeout(()=>host.classList.remove('shake'),180); return; }
          if(currentNum !== num){ say('Ese no es el número correcto.'); host.classList.add('shake'); setTimeout(()=>host.classList.remove('shake'),180); return; }
          // pinta
          el.style.fill = COLOR_MAP[num] || '#888';
          const z = zones.find(z=>z.el===el);
          if(!z.filled){ z.filled = true; filledCount++; updateProgress(); }
        }, {passive:true});
      });

      totalZones = zones.length;
      updateProgress();

      // Coloca números centrados automáticamente (si no existen)
      // (Calcula bbox; si hay superposición natural del dibujo no podemos evitarlo al 100%,
      //  pero aumentamos legibilidad con trazo.)
      // Solo generamos si el SVG no trae ya textos con clase .zone-num
      const existingNums = svg.querySelectorAll('.zone-num');
      if(!existingNums.length){
        const g = document.createElementNS('http://www.w3.org/2000/svg','g');
        g.setAttribute('data-generated','nums');
        zones.forEach(({el, num})=>{
          try{
            const bb = el.getBBox();
            const cx = bb.x + bb.width/2;
            const cy = bb.y + bb.height/2;
            const t = document.createElementNS('http://www.w3.org/2000/svg','text');
            t.setAttribute('x', String(cx));
            t.setAttribute('y', String(cy));
            t.setAttribute('text-anchor','middle');
            t.setAttribute('alignment-baseline','middle');
            t.setAttribute('class','zone-num');
            t.textContent = String(num);
            g.appendChild(t);
          }catch(e){ /* algunos elementos sin bbox -> ignorar */ }
        });
        // Inserta arriba para que quede visible
        svg.appendChild(g);
      }

      // Selecciona por defecto el menor número
      const first = palette.querySelector('.swatch');
      if(first){ first.click(); }

    }).catch(err=>{
      host.innerHTML = '<div class="hint">Error cargando el SVG.</div>';
      console.error(err);
    });

    function updateProgress(){
      if(totalZones === 0){ pct.textContent = '0% completado'; bar.style.width = '0%'; return; }
      const p = Math.round((filledCount/totalZones)*100);
      bar.style.width = p + '%';
      pct.textContent = p + '% completado';
      if(p >= 100){
        setTimeout(()=>openModal(), 250);
      }
    }
  </script>
</body>
</html>
