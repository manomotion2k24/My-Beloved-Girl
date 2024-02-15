
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Interactive Heart</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <link rel="stylesheet" href="https://unpkg.com/@google/model-viewer/dist/model-viewer.css">
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
        font-size: 100px;
        color: red;
        display: none;
        z-index: 1000;
      }
      model-viewer {
        width: 100%;
        height: 500px;
      }
      .ar-button {
        position: fixed;
        top: 20px;
        right: 20px;
        z-index: 10;
        background-color: #f1f1f1;
        border: none;
        cursor: pointer;
        padding: 10px;
        border-radius: 5px;
      }
      @keyframes levitate {
        0%, 100% {
          transform: translateY(0);
        }
        50% {
          transform: translateY(-10px);
        }
      }
      .ar-button .hand {
        display: inline-block;
        animation: levitate 2s ease-in-out infinite;
      }
    </style>
</head>
<body>

<model-viewer id="iosModelViewer" src="poem.glb" ios-src="poem.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="4" alt="A 3D model of an avatar"></model-viewer>

<button class="ar-button"><span class="hand">✋</span> Activează modul AR</button>

<div id="touchHeart" class="big-heart">❤️</div>

<script>
  function createHeart() {
    const heart = document.createElement('div');
    heart.classList.add('heart');
    heart.textContent = '❤️';
    heart.style.left = Math.random() * 100 + 'vw';
    heart.style.animationDuration = Math.random() * 2 + 3 + 's';
    heart.style.fontSize = Math.random() * 20 + 10 + 'px';
    document.body.appendChild(heart);

    setTimeout(() => {
      heart.remove();
    }, 5000);
  }

  let intervalId = setInterval(createHeart, 300);
  setTimeout(() => { clearInterval(intervalId); }, 60000);

  document.body.addEventListener('touchstart', function() {
    const bigHeart = document.getElementById('touchHeart');
    bigHeart.style.display = 'block';
    setTimeout(() => { bigHeart.style.display = 'none'; }, 2000);
  });

  document.querySelector('.ar-button').addEventListener('click', () => {
    document.querySelector('model-viewer').activateAR();
  });

  document.querySelector('model-viewer').addEventListener('ar-status', (event) => {
    if (event.detail.status === 'session-started') {
      console.log("AR session started");
    } else if (event.detail.status === 'session-ended') {
      console.log("AR session ended");
    }
  });
</script>

</body>
</html>
