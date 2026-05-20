<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Línea Temporal UE</title>

<style>

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

body{
  font-family:Arial, sans-serif;
  background:#0f172a;
  color:#e2e8f0;
  overflow-x:hidden;
}

/* ================= EFECTOS VISUALES ================= */

.decoracion{
  position:fixed;
  top:0;
  width:250px;
  height:100vh;
  pointer-events:none;
  z-index:-1;
  opacity:0.4;
}

.decoracion-izquierda{
  left:0;
  background:
    radial-gradient(circle at center,
    rgba(59,130,246,0.35),
    transparent 70%);
  filter:blur(40px);
  animation:moverIzquierda 8s infinite alternate ease-in-out;
}

.decoracion-derecha{
  right:0;
  background:
    radial-gradient(circle at center,
    rgba(96,165,250,0.3),
    transparent 70%);
  filter:blur(50px);
  animation:moverDerecha 10s infinite alternate ease-in-out;
}

@keyframes moverIzquierda{
  from{
    transform:translateY(-20px);
  }
  to{
    transform:translateY(40px);
  }
}

@keyframes moverDerecha{
  from{
    transform:translateY(20px);
  }
  to{
    transform:translateY(-40px);
  }
}

/* ================= PARTÍCULAS ================= */

.particulas::before,
.particulas::after{
  content:'';
  position:fixed;
  width:100%;
  height:100%;
  top:0;
  left:0;
  pointer-events:none;
  background-image:
    radial-gradient(circle, rgba(255,255,255,0.12) 2px, transparent 2px);
  background-size:80px 80px;
  animation:particulasMove 40s linear infinite;
  z-index:-2;
}

.particulas::after{
  animation-duration:60s;
  opacity:0.5;
}

@keyframes particulasMove{
  from{
    transform:translateY(0);
  }
  to{
    transform:translateY(-200px);
  }
}

/* ================= TRANSICIONES ================= */

.fade-out{
  animation:fadeOut 1s forwards;
}

.fade-in{
  animation:fadeIn 1s forwards;
}

@keyframes fadeOut{
  from{
    opacity:1;
    transform:scale(1);
  }
  to{
    opacity:0;
    transform:scale(1.05);
    visibility:hidden;
  }
}

@keyframes fadeIn{
  from{
    opacity:0;
    transform:scale(0.95);
  }
  to{
    opacity:1;
    transform:scale(1);
  }
}

/* ================= PANTALLAS ================= */

.pantalla{
  position:fixed;
  inset:0;
  background:#020617;
  display:flex;
  justify-content:center;
  align-items:center;
  z-index:9999;
  padding:20px;
}

.panel{
  background:#111827;
  border:1px solid #334155;
  padding:40px;
  border-radius:20px;
  max-width:600px;
  width:100%;
  text-align:center;
  box-shadow:0 0 30px rgba(0,0,0,0.5);
}

.panel h1{
  color:#60a5fa;
  margin-bottom:20px;
}

.panel p{
  margin-bottom:15px;
  line-height:1.6;
  color:#cbd5e1;
}

.panel button{
  margin-top:20px;
  padding:12px 25px;
  border:none;
  border-radius:10px;
  background:#2563eb;
  color:white;
  cursor:pointer;
  font-size:1rem;
  font-weight:bold;
  transition:0.3s;
}

.panel button:hover{
  background:#3b82f6;
}

/* ================= HEADER ================= */

header{
  background:linear-gradient(90deg,#111827,#1e293b);
  padding:30px;
  text-align:center;
  border-bottom:2px solid #334155;
  position:sticky;
  top:0;
  z-index:100;
}

header h1{
  color:#60a5fa;
  margin-bottom:10px;
}

.contador{
  margin-top:15px;
  background:#1e293b;
  display:inline-block;
  padding:10px 20px;
  border-radius:10px;
  border:1px solid #334155;
}

/* ================= TIMELINE ================= */

.timeline{
  position:relative;
  max-width:1100px;
  margin:50px auto;
  padding:20px 0;
}

.timeline::after{
  content:'';
  position:absolute;
  width:6px;
  background:#3b82f6;
  top:0;
  bottom:0;
  left:50%;
  margin-left:-3px;
}

.container{
  padding:10px 40px;
  position:relative;
  width:50%;
}

.left{
  left:0;
}

.right{
  left:50%;
}

.content{
  background:#1e293b;
  padding:25px;
  border-radius:15px;
  border:1px solid #334155;
  box-shadow:0 0 15px rgba(0,0,0,0.4);
  transition:0.4s;
}

.content:hover{
  transform:scale(1.02);
}

.container::after{
  content:'';
  position:absolute;
  width:22px;
  height:22px;
  background:#0f172a;
  border:4px solid #3b82f6;
  border-radius:50%;
  top:30px;
  z-index:10;
}

.left::after{
  right:-11px;
}

.right::after{
  left:-11px;
}

h2{
  color:#60a5fa;
  margin-bottom:10px;
}

/* ================= PREGUNTAS ================= */

.pregunta{
  margin-top:15px;
}

button{
  margin-top:10px;
  margin-right:10px;
  padding:10px 15px;
  border:none;
  border-radius:8px;
  background:#2563eb;
  color:white;
  cursor:pointer;
  transition:0.3s;
  font-weight:bold;
}

button:hover{
  background:#3b82f6;
}

button:disabled{
  background:#475569;
  cursor:not-allowed;
}

.resultado{
  margin-top:15px;
  font-weight:bold;
  font-size:1.1rem;
}

.correcto{
  color:#22c55e;
}

.incorrecto{
  color:#ef4444;
}

/* ================= BLOQUES INFORMATIVOS ================= */

.info-extra{
  background:#172554;
  border:1px solid #3b82f6;
  padding:25px;
  border-radius:15px;
  box-shadow:0 0 20px rgba(59,130,246,0.2);
}

.info-extra h3{
  color:#93c5fd;
  margin-bottom:10px;
}

.info-extra p{
  color:#dbeafe;
  line-height:1.6;
}

/* ================= FINAL ================= */

#pantallaFinal{
  display:none;
}

.resultadoFinal{
  font-size:2rem;
  color:#60a5fa;
  margin:20px 0;
}

/* ================= RESPONSIVE ================= */

@media screen and (max-width:768px){

  .timeline::after{
    left:31px;
  }

  .container{
    width:100%;
    padding-left:70px;
    padding-right:25px;
  }

  .container::after{
    left:15px;
  }

  .right{
    left:0;
  }

}

</style>
</head>

<body>

<div class="decoracion decoracion-izquierda"></div>
<div class="decoracion decoracion-derecha"></div>
<div class="particulas"></div>

<!-- PANTALLA INICIO -->

<div class="pantalla" id="pantallaInicio">

  <div class="panel">

    <h1>Historia de la Unión Europea</h1>

    <p>
      Recorre la línea temporal y responde preguntas sobre
      los momentos más importantes de la UE.
    </p>

    <button onclick="iniciarActividad()">
      Comenzar
    </button>

  </div>

</div>

<!-- PANTALLA FINAL -->

<div class="pantalla" id="pantallaFinal">

  <div class="panel">

    <h1>Actividad completada</h1>

    <div class="resultadoFinal">
      ✅ <span id="resultadoFinal">0</span> / 15
    </div>

    <p id="mensajeFinal"></p>

    <button onclick="location.reload()">
      Repetir actividad
    </button>

  </div>

</div>

<header>

  <h1>Línea Temporal de la UE</h1>

  <div class="contador">
    ✅ Aciertos:
    <span id="aciertos">0</span>
    / 15
  </div>

</header>

<div class="timeline">

<script>

const eventos = [
  ["1951","¿Qué organización nació aquí?","CECA","OTAN"],
  ["1957","¿Dónde se firmaron estos tratados?","Roma","Berlín"],
  ["1973","¿Qué país entró en esta ampliación?","Irlanda","España"],

  ["INFO","Dato curioso","La bandera de la Unión Europea tiene 12 estrellas porque simbolizan unidad y perfección."],

  ["1981","¿Qué país ingresó ese año?","Grecia","Portugal"],
  ["1985","¿Qué facilita este acuerdo?","Libre circulación","Nueva moneda"],
  ["1986","¿Qué países entraron ese año?","España y Portugal","Italia y Francia"],

  ["INFO","Información","El Parlamento Europeo es elegido directamente por los ciudadanos desde 1979."],

  ["1992","¿Qué nació oficialmente en 1992?","UE","ONU"],
  ["1999","¿Qué moneda apareció?","Euro","Franco"],
  ["2002","¿Cuándo empezó el euro físico?","2002","1990"],

  ["INFO","Sabías que...","El euro es una de las monedas más utilizadas e importantes del mundo."],

  ["2004","¿Cuántos países entraron en esta ampliación?","10","4"],
  ["2007","¿Qué tratado reformó la UE?","Lisboa","Versalles"],
  ["2009","¿Qué tratado entró en vigor?","Lisboa","Roma"],

  ["INFO","Dato histórico","La Unión Europea recibió el Premio Nobel de la Paz en 2012."],

  ["2012","¿Qué premio recibió la UE?","Nobel de la Paz","Óscar"],
  ["2013","¿Qué país ingresó ese año?","Croacia","Serbia"],
  ["2020","¿Qué país abandonó la UE?","Reino Unido","Suiza"]
];

let contadorPreguntas = 0;

document.write(

  eventos.map((e,i)=>{

    if(e[0] === "INFO"){

      return `

      <div class="container ${i%2===0 ? 'left' : 'right'}">

        <div class="content info-extra">

          <h3>${e[1]}</h3>

          <p>${e[2]}</p>

        </div>

      </div>

      `;
    }

    contadorPreguntas++;

    const correctoIzquierda = Math.random() > 0.5;

    const boton1 = correctoIzquierda
      ? `<button onclick="responder(this,true,${contadorPreguntas})">${e[2]}</button>`
      : `<button onclick="responder(this,false,${contadorPreguntas})">${e[3]}</button>`;

    const boton2 = correctoIzquierda
      ? `<button onclick="responder(this,false,${contadorPreguntas})">${e[3]}</button>`
      : `<button onclick="responder(this,true,${contadorPreguntas})">${e[2]}</button>`;

    return `

    <div class="container ${i%2===0 ? 'left' : 'right'}">

      <div class="content">

        <h2>${e[0]}</h2>

        <div class="pregunta">

          <p><strong>${e[1]}</strong></p>

          ${boton1}
          ${boton2}

          <div id="resultado${contadorPreguntas}" class="resultado"></div>

        </div>

      </div>

    </div>

    `;

  }).join('')

);

</script>

</div>

<script>

let aciertos = 0;
let respondidas = {};
let totalRespondidas = 0;

const totalPreguntas = 15;

/* ================= INICIO ================= */

function iniciarActividad(){

  const pantallaInicio = document.getElementById("pantallaInicio");

  pantallaInicio.classList.add("fade-out");

  setTimeout(() => {

    pantallaInicio.style.display = "none";

  }, 900);

}

/* ================= RESPUESTAS ================= */

function responder(boton, correcto, id){

  if(respondidas[id]) return;

  respondidas[id] = true;

  totalRespondidas++;

  const resultado = document.getElementById("resultado" + id);

  const botones = boton.parentElement.querySelectorAll("button");

  botones.forEach(btn => {
    btn.disabled = true;
  });

  if(correcto){

    aciertos++;

    document.getElementById("aciertos").innerText = aciertos;

    resultado.innerHTML = "✅ Correcto";
    resultado.classList.add("correcto");

  } else {

    resultado.innerHTML = "❌ Incorrecto";
    resultado.classList.add("incorrecto");

  }

  comprobarFinal();

}

/* ================= FINAL ================= */

function comprobarFinal(){

  if(totalRespondidas === totalPreguntas){

    document.getElementById("resultadoFinal").innerText = aciertos;

    let mensaje = "";

    if(aciertos <= 5){

      mensaje = "Sigue practicando la historia de la UE.";

    } else if(aciertos <= 10){

      mensaje = "Buen trabajo.";

    } else {

      mensaje = "Excelente resultado.";

    }

    document.getElementById("mensajeFinal").innerText = mensaje;

    const pantallaFinal = document.getElementById("pantallaFinal");

    pantallaFinal.style.display = "flex";

    pantallaFinal.classList.add("fade-in");

    document.body.style.overflow = "hidden";

    window.scrollTo({
      top:0,
      behavior:"smooth"
    });

  }

}

</script>

</body>
</html>
