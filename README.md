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
        font-size: 100px;
        color: red;
        display: none;
        z-index: 1000;
      }
      model-viewer {
        width: 100%;
        height: 500px;
      }
      @keyframes levitate {
        0%, 100% {
          transform: translateY(0);
        }
        50% {
          transform: translateY(-5px);
        }
      }
      .levitate {
        display: inline-block; /* Asigură-te că span-ul poate fi transformat */
        animation: levitate 1s ease-in-out infinite;
      }
    </style>
</head>
<body>

<model-viewer ar camera-controls touch-action="pan-y" src="poem.glb" alt="A 3D model">
  <button slot="ar-button" class="ar-button" style="background-color: white; border-radius: 4px; border: none; position: absolute; top: 16px; right: 16px; ">
      <span class="levitate">👋</span> Activează modul AR
  </button>
</model-viewer>

<div id="touchHeart" class="big-heart">❤️</div>

<script>
  // Script pentru crearea inimioarelor și logica pentru inima mare așa cum a fost descris anterior
</script>

</body>
</html>
