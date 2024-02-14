Mulțumesc pentru că ești! 
I love YOU!
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Falling Hearts</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <style>
      @keyframes fall {
        to { transform: translateY(100vh); }
      }
      .heart {
        position: fixed;
        top: -100px;
        color: red; /* Culoarea inimioarelor */
        animation: fall linear;
      }
      /* Ascundem model-viewer-ul inițial pentru a-l afișa doar pe iOS */
      model-viewer {
        display: none;
      }
    </style>
</head>
<body>

<!-- Mesaj pentru utilizatorii de iOS -->
<p id="iosMessage" style="display: none;">Deschide în Safari dacă ești pe Apple</p>

<!-- Link înapoi la pagina produsului -->
<p><a href="https://vimeo.com/user74836700">Înapoi la pagina produsului</a></p>

<!-- Vizualizatorul de model 3D -->
<model-viewer id="iosModelViewer" src="poem5.glb" ios-src="poem5.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="1" alt="A 3D model of an avatar"></model-viewer>

<script>
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
        if (navigator.platform === iDevices.pop()){ 
          document.getElementById('iosMessage').style.display = 'block';
          // Afișăm model-viewer doar pe dispozitivele iOS
          document.getElementById('iosModelViewer').style.display = 'block';
          return true; 
        }
      }
    }
    return false;
  }

  checkIfIOS(); // Verificăm dacă utilizatorul este pe iOS la încărcarea paginii

  // Codul pentru inimioare rămâne neschimbat
  function createHeart() {
    // Restul funcției createHeart
  }

  // Inițierea inimioarelor care cad
  let intervalId = setInterval(createHeart, 300);
  setTimeout(() => { clearInterval(intervalId); }, 60000);
</script>

</body>
</html>
