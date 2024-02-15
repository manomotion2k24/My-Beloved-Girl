Bucura-te de acest model 3D la tine in camera
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model View with Interactive Heart</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <script type="module" src="https://unpkg.com/@google/model-viewer"></script>
    <style>
      body {
        font-family: 'Roboto', sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f0f0f0; /* Un fundal mai deschis pentru un look fresh */
        overflow-x: hidden;
      }

      @keyframes fall {
        0% { transform: translateY(-100px); }
        100% { transform: translateY(100vh); }
      }

      @keyframes fadeInOut {
        0%, 100% { opacity: 0; }
        50% { opacity: 1; }
      }

      .heart {
        position: fixed;
        color: red;
        animation: fall linear, fadeInOut 5s linear;
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
        animation: fadeInOut 2s linear;
      }

      model-viewer {
        width: 100%;
        height: 500px;
        transition: height 0.5s ease-in-out; /* Smooth transition for responsive adjustments */
      }

      @media (max-width: 768px) {
        model-viewer {
          height: 300px; /* Adjust for smaller devices */
        }
      }
    </style>
</head>
<body>

<model-viewer id="iosModelViewer" src="poem.glb" ios-src="poem.usdz" ar ar-modes="webxr scene-viewer quick-look" camera-controls auto-rotate environment-image="neutral" shadow-intensity="4" alt="A 3D model of an avatar"></model-viewer>

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
  setTimeout(() => { clearInterval(intervalId); }, 60000); // Corectat la 60 de secunde

  document.body.addEventListener('touchstart', showBigHeart);
  document.body.addEventListener('click', showBigHeart); // Adaugat suport pentru dispozitivele fara touch

  function showBigHeart() {
    const bigHeart = document.getElementById('touchHeart');
    bigHeart.style.display = 'block';
    setTimeout(() => { bigHeart.style.display = 'none'; }, 2000);
  }
</script>

</body>
</html>
