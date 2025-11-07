<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Feliz Cumpleaños Luz</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap');

  body {
    margin: 0;
    padding: 0;
    overflow: hidden;
    font-family: 'Dancing Script', cursive;
  }

  .screen {
    width: 100%;
    height: 100vh;
    display: none;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    text-align: center;
    position: relative;
    opacity: 0;
    transition: opacity 1s ease;
  }

  .screen.show { display: flex; opacity: 1; }

  /* --- PANTALLA 1 --- */
  #screen1 {
    background: url('https://img.freepik.com/premium-photo/photo-might-starry-sky-wallpaper_948544-36443.jpg') no-repeat center center/cover;
    color: white;
    overflow: hidden;
  }

  #screen1 h1 {
    font-size: 2em;
    line-height: 1.4em;
    max-width: 80%;
    opacity: 0;
    animation: fadeIn 3s ease forwards;
    text-shadow: 2px 2px 6px rgba(0,0,0,0.7);
  }

  #screen1 .continue {
    margin-top: 40px;
    font-size: 1.5em;
    cursor: pointer;
    opacity: 0;
    animation: fadeIn 3s 3s ease forwards;
    transition: transform 0.3s;
    text-shadow: 2px 2px 6px rgba(0,0,0,0.7);
  }

  #screen1 .continue:hover { transform: scale(1.1); }

  #screen1 .rain { position: absolute; top:0; left:0; width:100%; height:100%; pointer-events: none; overflow: hidden; }
  .drop { position: absolute; bottom:100%; width:2px; height:15px; background:rgba(255,255,255,0.3); animation: fall 1s linear infinite; }

  /* --- PANTALLA 2 --- */
  #screen2 {
    background: url('https://www.tunecore.co.jp/s3pna/tcj-image-production/u366922/r1135533/itd1135533.png') no-repeat center center/cover;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: black;
  }

  #screen2 h1 { font-size: 2.2em; opacity: 0; animation: fadeInScreen2 3s forwards; text-shadow: 2px 2px 8px rgba(255,255,255,0.7); }
  #screen2 .small-image { position: absolute; bottom: 20px; right: 20px; width: 200px; border-radius: 15px; box-shadow: 0 0 15px rgba(0,0,0,0.5); }
  #screen2 .musical-notes { position: absolute; top: 10%; left: 50%; transform: translateX(-50%); font-size: 1.5em; animation: notesFloat 4s infinite alternate; }
  #screen2 .adelante { position: absolute; bottom: 50px; left: 50%; transform: translateX(-50%); font-size: 1.8em; cursor: pointer; opacity: 0; animation: fadeInAdelante 3s 1s forwards; text-shadow: 2px 2px 8px rgba(255,255,255,0.7); }

  /* --- PANTALLA 3 --- */
  #screen3 {
    background: url('https://d.wattpad.com/story_parts/67/images/14028a5cfb9209af.jpg') no-repeat center center/cover;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    padding: 0 20px;
  }

  #screen3 h1 { font-size: 2em; opacity: 0; animation: fadeInScreen3 3s forwards; text-shadow: 2px 2px 8px rgba(0,0,0,0.7); margin-bottom: 20px; }
  #screen3 p { font-size: 1.2em; opacity: 0; animation: fadeInScreen3 3s 1s forwards; text-shadow: 2px 2px 8px rgba(0,0,0,0.7); line-height: 1.5em; margin-bottom: 40px; }
  #screen3 .birthday-button { font-size: 1.8em; cursor: pointer; padding: 10px 25px; border: 2px solid white; border-radius: 10px; transition: transform 0.3s, background-color 0.3s; }
  #screen3 .birthday-button:hover { transform: scale(1.1); background-color: rgba(255,255,255,0.2); }

  /* --- PANTALLA 4 --- */
  #screen4 {
    background: url('https://img.freepik.com/fotos-premium/superficie-luna-paisaje-lunar-espectacular-terreno-crateres-rocas-esteriles_1089554-7713.jpg') no-repeat center center/cover;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    color: white;
    overflow-y: auto;
    padding: 30px;
  }

  #screen4 h1 { font-size: 2.2em; text-shadow: 2px 2px 10px rgba(0,0,0,0.7); margin-bottom: 20px; }
  #screen4 .message-box { max-width: 700px; background-color: rgba(0,0,0,0.5); padding: 25px; border-radius: 15px; font-size: 1.2em; line-height: 1.5em; text-shadow: 1px 1px 4px rgba(0,0,0,0.7); position: relative; }
  #screen4 .signature { position: absolute; bottom: 10px; right: 15px; font-size: 1em; color: rgba(255,255,255,0.6); font-style: italic; }
  #screen4 .rain4 { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; overflow: hidden; }

  /* --- BOTÓN DE MÚSICA --- */
  #musicButton {
    position: fixed;
    top: 15px;
    right: 15px;
    background-color: rgba(0,0,0,0.5);
    color: white;
    border: none;
    border-radius: 50%;
    font-size: 1.5em;
    width: 45px;
    height: 45px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 8px rgba(255,255,255,0.3);
    transition: transform 0.3s, background-color 0.3s;
    z-index: 1000;
  }

  #musicButton:hover { transform: scale(1.1); background-color: rgba(255,255,255,0.2); }

  /* --- ANIMACIONES --- */
  @keyframes fadeIn { from {opacity:0; transform:translateY(20px);} to {opacity:1; transform:translateY(0);} }
  @keyframes fall { to {transform:translateY(100vh);} }
  @keyframes notesFloat { from {transform:translate(-50%,0);} to {transform:translate(-50%,-20px);} }
  @keyframes fadeInScreen2 { from {opacity:0; transform:translateY(-20px);} to {opacity:1; transform:translateY(0);} }
  @keyframes fadeInAdelante { from {opacity:0; transform:translateY(20px);} to {opacity:1; transform:translateY(0);} }
  @keyframes fadeInScreen3 { from {opacity:0; transform:translateY(-20px);} to {opacity:1; transform:translateY(0);} }
</style>
</head>
<body>

<!-- PANTALLAS -->
<div class="screen show" id="screen1">
  <h1>El tiempo pasa, más rápido de lo que imaginamos.<br>Pero no olvidaría este día.</h1>
  <div class="continue" onclick="showScreen('screen2')">¿Continuas?</div>
  <div class="rain" id="rain"></div>
</div>

<div class="screen" id="screen2">
  <div class="musical-notes">🎵 🎶 🎵</div>
  <h1>Feliz Cumpleaños Luz</h1>
  <img src="https://2.bp.blogspot.com/-AAKHPHiKIZE/UdDCcFA4PPI/AAAAAAAACfQ/ib_L8wTq50I/s1600/CAM01126.jpg" class="small-image" alt="Foto pequeña">
  <div class="adelante" onclick="showScreen('screen3')">Adelante</div>
</div>

<div class="screen" id="screen3">
  <h1>Entre Notas y Recuerdos</h1>
  <p>La noche es bella más cuando la luna está llena, tan lejos y tan cerca de los pensamientos que simplemente con saber que está ahí, lo hace más bello aún. La Luna hace que la noche sea especial porque ilumina la noche con su poca iluminación y se luce en la noche más oscura.</p>
  <div class="birthday-button" onclick="showScreen('screen4')">Feliz Cumpleaños</div>
</div>

<div class="screen" id="screen4">
  <h1>Feliz Cumpleaños Luz</h1>
  <div class="message-box">
    <p>Hoy pensé en ti. No por costumbre, ni por nostalgia, sino porque el calendario me recordó que este día siempre fue especial.</p>
    <p>Aunque el tiempo haya seguido su curso y nuestras vidas se hayan distanciado, hay cosas que no se olvidan, y una de ellas es desearte lo mejor en tu cumpleaños.</p>
    <p>No sé en qué punto del camino te encuentras ahora, pero me gusta imaginarte bien: rodeada de personas que te quieren, sonriendo con esa calma que alguna vez soñaste alcanzar. Ojalá la vida haya sido amable contigo, que el tiempo te haya regalado momentos de paz, y que sigas encontrando razones para reír sin mirar atrás.</p>
    <p>A veces pienso que dejar ir también fue una forma de cuidarte, de permitir que cada uno siguiera creciendo en paz. Y aunque nuestras palabras se apagaron con el tiempo, el cariño que guardo no se marchitó; solo aprendió a quedarse en silencio, como una melodía que ya no suena, pero aún se recuerda.</p>
    <p>Hoy no busco más que eso: que sepas, aunque no lo leas, que alguien te desea un feliz cumpleaños con un corazón tranquilo y agradecido.</p>
    <p>Que este nuevo año te encuentre en armonía, rodeada de amor sincero, de amaneceres suaves y de pequeñas alegrías que te hagan sentir viva.</p>
    <p>Feliz cumpleaños.</p>
    <p>Desde lejos, pero con afecto,<br>alguien que aún Te Desea Lo Mejor.</p>
    <div class="signature">Vlady</div>
  </div>
  <div class="rain4" id="rain4"></div>
</div>

<!-- Música -->
<audio id="bgMusic" loop>
  <source src="musica.mp3" type="audio/mp3">
  Tu navegador no soporta el elemento de audio.
</audio>

<!-- Botón de música -->
<button id="musicButton" onclick="toggleMusic()">🔇</button>

<script>
const music = document.getElementById('bgMusic');
const musicButton = document.getElementById('musicButton');
let musicStarted = false;
music.volume = 0.5;

function createRain(containerId, dropClass){
  const rainContainer=document.getElementById(containerId);
  for(let i=0;i<50;i++){
    const drop=document.createElement('div');
    drop.classList.add(dropClass);
    drop.style.left=Math.random()*100+'vw';
    drop.style.animationDuration=(0.5+Math.random()*0.7)+'s';
    drop.style.animationDelay=Math.random()*2+'s';
    rainContainer.appendChild(drop);
  }
}

function showScreen(screenId){
  const current=document.querySelector('.screen.show');
  current.classList.remove('show');
  setTimeout(()=>{
    current.style.display='none';
    const next=document.getElementById(screenId);
    next.style.display='flex';
    next.classList.add('show');
    if(screenId==='screen1') createRain('rain','drop');
    if(screenId==='screen4') createRain('rain4','drop4');
  },500);

  // Reproducir música al primer clic
  if (!musicStarted) {
    music.play().then(()=>{
      musicButton.textContent = '🔊';
    }).catch(()=>{});
    musicStarted = true;
  }
}

function toggleMusic(){
  if(music.paused){
    music.play();
    musicButton.textContent = '🔊';
  } else {
    music.pause();
    musicButton.textContent = '🔇';
  }
}

// Iniciar lluvia
createRain('rain','drop');
</script>
</body>
</html>
