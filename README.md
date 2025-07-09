<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SoulMuse 🌟</title>
  <link rel="stylesheet" href="style.css" />
  <style>
    body {
      font-family: 'Courier New', cursive;
      background: linear-gradient(to right, #f9f7f7, #fcefee);
      color: #333;
      padding: 20px;
      text-align: center;
    }
    section {
      margin: 2rem auto;
      max-width: 600px;
      background: #ffffffaa;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    input, textarea, button {
      display: block;
      margin: 10px auto;
      padding: 10px;
      border-radius: 10px;
      border: 1px solid #ccc;
      width: 80%;
    }
    textarea {
      height: 100px;
    }
    .hidden {
      display: none;
    }
    .actions button {
      display: inline-block;
      margin: 0 10px;
    }
    #results {
      margin-top: 20px;
      padding: 10px;
      background: #eee;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <!-- Pantalla de inicio -->
  <section id="start-screen">
    <h1>🌟 App: SoulMuse</h1>
    <p>Tu compañera creativa con IA que transforma emociones en arte.</p>
    <button onclick="showLogin()">Iniciar sesión</button>
    <button onclick="showRegister()">Registrarse</button>
  </section>

  <!-- Pantalla de inicio de sesión -->
  <section id="login-screen" class="hidden">
    <h2>Iniciar sesión</h2>
    <input type="email" placeholder="Email" id="login-email">
    <input type="password" placeholder="Contraseña" id="login-password">
    <button onclick="login()">Entrar</button>
  </section>

  <!-- Pantalla de registro -->
  <section id="register-screen" class="hidden">
    <h2>Registrarse</h2>
    <input type="text" placeholder="Nombre" id="register-name">
    <input type="email" placeholder="Email" id="register-email">
    <input type="password" placeholder="Contraseña" id="register-password">
    <button onclick="register()">Crear cuenta</button>
  </section>

  <!-- Pantalla principal -->
  <section id="main-app" class="hidden">
    <h2>Bienvenido/a a SoulMuse</h2>
    <textarea id="userInput" placeholder="¿Cómo te sientes hoy?"></textarea>
    <div class="actions">
      <button onclick="generateArt()">🎨 Generar Arte</button>
      <button onclick="generateMusic()">🎵 Generar Música</button>
      <button onclick="generatePoem()">✍️ Generar Poema</button>
    </div>

    <div id="results"></div>

    <h3>MoodMirror</h3>
    <button onclick="openCamera()">🎭 Escanear Rostro</button>
    <button onclick="recordVoice()">🎙️ Grabar Voz</button>
    <video id="camera" autoplay muted class="hidden"></video>
    <audio id="voice-record" controls class="hidden"></audio>

    <button onclick="linkSpotify()">🎧 Vincular con Spotify</button>
  </section>

  <script>
    function showLogin() {
      document.getElementById('start-screen').classList.add('hidden');
      document.getElementById('login-screen').classList.remove('hidden');
    }

    function showRegister() {
      document.getElementById('start-screen').classList.add('hidden');
      document.getElementById('register-screen').classList.remove('hidden');
    }

    function login() {
      // Aquí iría lógica real
      document.getElementById('login-screen').classList.add('hidden');
      document.getElementById('main-app').classList.remove('hidden');
    }

    function register() {
      // Aquí iría lógica real
      document.getElementById('register-screen').classList.add('hidden');
      document.getElementById('main-app').classList.remove('hidden');
    }

    function generateArt() {
      const text = document.getElementById('userInput').value;
      document.getElementById('results').innerText = `🎨 Generando arte basado en: "${text}"`;
    }

    function generateMusic() {
      const text = document.getElementById('userInput').value;
      document.getElementById('results').innerText = `🎵 Generando música basada en: "${text}"`;
    }

    function generatePoem() {
      const text = document.getElementById('userInput').value;
      document.getElementById('results').innerText = `✍️ Generando poema basado en: "${text}"`;
    }

    function openCamera() {
      const video = document.getElementById('camera');
      navigator.mediaDevices.getUserMedia({ video: true })
        .then(stream => {
          video.classList.remove('hidden');
          video.srcObject = stream;
        })
        .catch(err => alert('No se pudo acceder a la cámara'));
    }

    function recordVoice() {
      const audio = document.getElementById('voice-record');
      navigator.mediaDevices.getUserMedia({ audio: true })
        .then(stream => {
          const mediaRecorder = new MediaRecorder(stream);
          const chunks = [];

          mediaRecorder.ondataavailable = e => chunks.push(e.data);
          mediaRecorder.onstop = () => {
            const blob = new Blob(chunks, { type: 'audio/mp3' });
            audio.src = URL.createObjectURL(blob);
            audio.classList.remove('hidden');
          };

          mediaRecorder.start();
          setTimeout(() => mediaRecorder.stop(), 3000);
        })
        .catch(err => alert('No se pudo grabar audio'));
    }

    function linkSpotify() {
      alert('Redirigiendo a autenticación de Spotify...');
      // Aquí iría lógica de OAuth con Spotify API
    }
  </script>
</body>
</html>
