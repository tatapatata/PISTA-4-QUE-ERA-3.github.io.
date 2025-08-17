<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Pinta por números – Panda Rojo y Mapache</title>
  <style>
    body {
      background: #0d1b2a;
      color: white;
      text-align: center;
      font-family: Arial, sans-serif;
    }
    svg {
      width: 80%;
      max-width: 800px;
      margin: auto;
      display: block;
    }
    .palette {
      margin-top: 20px;
    }
    .color-btn {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      border: 2px solid white;
      display: inline-block;
      margin: 5px;
      cursor: pointer;
    }
    #qr {
      display: none;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Pinta por números</h1>
  <p>Elige un color y pinta las zonas con su número.<br>Al terminar, tendrás una sorpresa.</p>

  <!-- Dibujo base en SVG -->
  <svg id="paint-area" viewBox="0 0 600 400">

    <!-- Panda Rojo (izquierda) -->
    <ellipse class="zone" id="panda-head" cx="180" cy="120" rx="80" ry="100" data-num="1" fill="white" stroke="black"/>
    <ellipse class="zone" id="panda-body" cx="180" cy="260" rx="100" ry="120" data-num="2" fill="white" stroke="black"/>
    <ellipse class="zone" id="panda-belly" cx="180" cy="270" rx="60" ry="80" data-num="3" fill="white" stroke="black"/>
    <ellipse class="zone" id="panda-ear-left" cx="120" cy="50" rx="30" ry="30" data-num="4" fill="white" stroke="black"/>
    <ellipse class="zone" id="panda-ear-right" cx="240" cy="50" rx="30" ry="30" data-num="4" fill="white" stroke="black"/>
    <ellipse class="zone" id="panda-tail" cx="280" cy="300" rx="25" ry="40" data-num="5" fill="white" stroke="black"/>
    <text x="180" y="120" text-anchor="middle" fill="black" font-size="20">1</text>
    <text x="180" y="260" text-anchor="middle" fill="black" font-size="20">2</text>
    <text x="180" y="270" text-anchor="middle" fill="black" font-size="20">3</text>
    <text x="120" y="50" text-anchor="middle" fill="black" font-size="20">4</text>
    <text x="240" y="50" text-anchor="middle" fill="black" font-size="20">4</text>
    <text x="280" y="300" text-anchor="middle" fill="black" font-size="20">5</text>

    <!-- Mapache (derecha) -->
    <ellipse class="zone" id="raccoon-head" cx="420" cy="120" rx="80" ry="100" data-num="6" fill="white" stroke="black"/>
    <ellipse class="zone" id="raccoon-body" cx="420" cy="260" rx="100" ry="120" data-num="7" fill="white" stroke="black"/>
    <ellipse class="zone" id="raccoon-belly" cx="420" cy="270" rx="60" ry="80" data-num="8" fill="white" stroke="black"/>
    <path class="zone" id="raccoon-mask" d="M340,120 Q420,60 500,120 Q420,180 340,120Z" data-num="9" fill="white" stroke="black"/>
    <ellipse class="zone" id="raccoon-ear-left" cx="360" cy="50" rx="30" ry="30" data-num="10" fill="white" stroke="black"/>
    <ellipse class="zone" id="raccoon-ear-right" cx="480" cy="50" rx="30" ry="30" data-num="10" fill="white" stroke="black"/>
    <ellipse class="zone" id="raccoon-tail" cx="520" cy="300" rx="25" ry="40" data-num="11" fill="white" stroke="black"/>
    <text x="420" y="120" text-anchor="middle" fill="black" font-size="20">6</text>
    <text x="420" y="260" text-anchor="middle" fill="black" font-size="20">7</text>
    <text x="420" y="270" text-anchor="middle" fill="black" font-size="20">8</text>
    <text x="420" y="120" text-anchor="middle" fill="black" font-size="20">9</text>
    <text x="360" y="50" text-anchor="middle" fill="black" font-size="20">10</text>
    <text x="480" y="50" text-anchor="middle" fill="black" font-size="20">10</text>
    <text x="520" y="300" text-anchor="middle" fill="black" font-size="20">11</text>

    <!-- Manos unidas -->
    <ellipse class="zone" id="hands" cx="300" cy="250" rx="40" ry="40" data-num="12" fill="white" stroke="black"/>
    <text x="300" y="250" text-anchor="middle" fill="black" font-size="20">12</text>
  </svg>

  <!-- Paleta de colores -->
  <div class="palette">
    <div class="color-btn" style="background:#e63946" data-color="#e63946"></div>
    <div class="color-btn" style="background:#f1faee" data-color="#f1faee"></div>
    <div class="color-btn" style="background:#a8dadc" data-color="#a8dadc"></div>
    <div class="color-btn" style="background:#ffb703" data-color="#ffb703"></div>
    <div class="color-btn" style="background:#457b9d" data-color="#457b9d"></div>
    <div class="color-btn" style="background:#2a9d8f" data-color="#2a9d8f"></div>
    <div class="color-btn" style="background:#8d99ae" data-color="#8d99ae"></div>
    <div class="color-btn" style="background:#6d6875" data-color="#6d6875"></div>
    <div class="color-btn" style="background:#1d3557" data-color="#1d3557"></div>
  </div>

  <!-- QR sorpresa -->
  <img id="qr" src="aaaaaaaaaaaaaaaaaaaaaaaaaaaa.png" width="200" alt="QR Spotify">

  <script>
    let currentColor = null;

    document.querySelectorAll(".color-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        currentColor = btn.dataset.color;
      });
    });

    document.querySelectorAll(".zone").forEach(zone => {
      zone.addEventListener("click", () => {
        if(currentColor){
          zone.setAttribute("fill", currentColor);
          checkCompletion();
        }
      });
    });

    function checkCompletion(){
      const zones = document.querySelectorAll(".zone");
      let allColored = true;
      zones.forEach(z => {
        if(z.getAttribute("fill") === "white"){
          allColored = false;
        }
      });
      if(allColored){
        document.getElementById("qr").style.display = "block";
      }
    }
  </script>
</body>
</html>
