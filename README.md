Mulțumesc pentru că ești! I love YOU!
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Falling Hearts</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <style>
      @keyframes fall {
        to {
          transform: translateY(100vh);
        }
      }
      .heart {
        position: fixed;
        top: -100px;
        color: red; /* Culoarea inimioarelor */
        animation: fall linear;
      }
    </style>
</head>
<body>

<!-- Mesaj pentru utilizatorii de iOS -->
<p id="iosMessage" style="display: none;">Deschide în Safari dacă ești pe Apple</p>

<!-- Link înapoi la pagina produsului -->
<p><a href="https://vimeo.com/user74836700">Înapoi la pagina produsului</a></p>

<!-- Vizualizatorul de model 3D -->
<model-viewer src="Poem5.glb" ios-src="Poem5.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="1" alt="A 3D model of an avatar"></model-viewer>

<script>
  // Funcție pentru a verifica dacă utilizatorul este pe un dispozitiv iOS
  function checkIfIOS() {
    var iDevices = [
      'iPad Simulator',
      'iPhone Simulator',
      'iPod Simulator',
      'iPad',
      'iPhone',
      'iPod'
    ];

    if (!!navigator.platform) {
      while (iDevices.length) {
        if (navigator.platform === iDevices.pop()){ return true; }
      }
    }

    return false;
  }

  // Dacă este iOS, afișăm mesajul
  if(checkIfIOS()) {
    document.getElementById('iosMessage').style.display = 'block';
  }

  // Funcție pentru crearea inimioarelor care cad
  function createHeart() {
    const heart = document.createElement('div');
    heart.classList.add('heart');
    heart.textContent = '❤️'; // Emoji inimioară
    heart.style.left = Math.random() * 100 + 'vw';
    heart.style.animationDuration = Math.random() * 2 + 3 + 's'; // Durata între 3 și 5 secunde
    heart.style.fontSize = Math.random() * 20 + 10 + 'px'; // Mărimea între 10 și 30px
    document.body.appendChild(heart);

    // Elimină inimioara după ce a terminat de căzut
    setTimeout(() => {
      heart.remove();
    }, 5000); // Elimină inimioara după 5 secunde (durata maximă de animație)
  }

  // Rulează funcția createHeart pentru 60 de secunde
  let intervalId = setInterval(createHeart, 300); // Generează o inimioară la fiecare 300ms

  // Oprește generarea inimioarelor după 60 de secunde
  setTimeout(() => {
    clearInterval(intervalId);
  }, 60000); // 60 de secunde
</script>

</body>
</html>

