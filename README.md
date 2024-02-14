Mulțumesc pentru că ești! 
I love YOU!

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Interactive Heart</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <style>
      @keyframes fall {
        to { transform: translateY(100vh); }
      }
      .heart {
        position: fixed;
        top: -100px;
        color: red;
        animation: fall linear;
      }
      .big-heart {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 100px; /* Mărimea inimii mari */
        color: red;
        display: none;
      }
      model-viewer {
        display: block;
        width: 100%;
        height: 500px; /* Ajustează înălțimea după necesități */
      }
    </style>
</head>
<body>

<model-viewer id="iosModelViewer" src="Poem5.glb" ios-src="Poem5.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="1" alt="A 3D model of an avatar"></model-viewer>

<div id="touchHeart" class="big-heart">❤️</div>

<script>
  checkIfIOS(); // Verificăm dacă utilizatorul este pe iOS la încărcarea paginii

  function createHeart() {
    // Cod pentru generarea inimioarelor mici
  }

  // Inițierea inimioarelor care cad
  let intervalId = setInterval(createHeart, 300);
  setTimeout(() => { clearInterval(intervalId); }, 60000); // 60 de secunde

  // Funcție pentru afișarea inimii mari la atingerea ecranului
  document.body.addEventListener('touchstart', function() {
    const bigHeart = document.getElementById('touchHeart');
    bigHeart.style.display = 'block'; // Afișăm inima mare
    setTimeout(() => { bigHeart.style.display = 'none'; }, 2000); // Ascundem inima după 2 secunde
  });
</script>

</body>
</html>
