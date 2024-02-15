<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Interactive Heart and AR Support Check</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <style>
      @keyframes float {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-10px); }
      }
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
      #ar-button {
        background-color: white;
        border-radius: 4px;
        border: none;
        position: absolute;
        top: 16px;
        right: 16px;
        animation: float 2s ease-in-out infinite;
      }
      #error {
        background-color: #ffffffdd;
        border-radius: 16px;
        padding: 16px;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate3d(-50%, -50%, 0);
        transition: opacity 0.3s;
        visibility: hidden;
        opacity: 0;
      }
      #error.show {
        visibility: visible;
        opacity: 1;
      }
    </style>
</head>
<body>

<model-viewer id="model-viewer" src="poem.glb" ios-src="poem.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="4" alt="A 3D model of an avatar">
    <button id="ar-button" slot="ar-button">
        ✋ Activează modul AR
    </button>
    <div id="error" class="hide">AR is not supported on this device</div>
</model-viewer>

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

  document.querySelector('#model-viewer').addEventListener('ar-status', (event) => {
    if(event.detail.status === 'failed'){
      const error = document.querySelector("#error");
      error.classList.add('show');
      setTimeout(() => {
        error.classList.remove('show');
      }, 3000);
    }
  });
</script>

</body>
</html>
