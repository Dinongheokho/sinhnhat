<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Thiệp sinh nhật 💖</title>
  <style>
    * {
      transition: all 1 s ease;
    }
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(180deg, #ffe6f0, #ffd6eb, #fff0f6);
      font-family: 'Segoe UI', cursive, sans-serif;
      overflow: hidden;
      height: 100 vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: #d63384;
    }
    .intro {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #ffd6eb;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 10;
      transition: opacity 1s ease, visibility 1s ease;
    }
    .intro h2 {
      font-size: 2.5em;
      color: #ff4da6;
      animation: pulse 1.5s infinite;
      cursor: pointer;
      background: white;
      padding: 15px 40px;
      border-radius: 30px;
      box-shadow: 0 0 20px rgba(255, 128, 171, 0.6);
    }
    .intro.hidden {
      opacity: 0;
      visibility: hidden;
    }
    @keyframes pulse {
      0%, 100% { transform: scale(1); box-shadow: 0 0 15px rgba(255,128,171,0.8); }
      50% { transform: scale(1.1); box-shadow: 0 0 30px rgba(255,128,171,1); }
    }
    /* Thiệp */
    .card {
      background: rgba(255, 255, 255, 0.8);
      backdrop-filter: blur(8px);
      border-radius: 20px;
      padding: 40px 60px;
      text-align: center;
      box-shadow: 0 0 30px rgba(255, 192, 203, 0.6);
      position: relative;
      z-index: 2;
      opacity: 0;
      transform: scale(0.95);
    }
    .card.show {
      opacity: 1;
      transform: scale(1);
      transition: all 1.5s ease;
    }
    h1 {
      font-size: 2.5em;
      color: #ff4da6;
      margin-bottom: 10px;
      text-shadow: 0 0 10px #fff;
    }
    p {
      font-size: 1.2em;
      color: #cc3a8a;
      margin-bottom: 20px;
      line-height: 1.6;
    }
    /* Nút quà */
    .gift-btn {
      background: linear-gradient (45 deg, #ff66b2, #ff99cc);
      border: none;
      border-radius: 50%;
      width: 80 px;
      height: 80 px;
      cursor: pointer;
      box-shadow: 0 0 15 px rgba (255, 128, 171, 0.7);
      animation: pulse 1.5 s infinite;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      z-index: 3;
      opacity: 0;
      transition: opacity 1 s ease;
    }
    .gift-btn.show {
      opacity: 1;
    }
    .gift-btn img {
      width: 45 px;
      height: 45 px;
    }
    /* Ảnh hiện lên */
    .popup {
      position: fixed;
      top: 50 %;
      left: 50 %;
      transform: translate (-50 %, -50 %) scale (0);
      background: rgba (255,255,255,0.9);
      padding: 20 px;
      border-radius: 15 px;
      box-shadow: 0 0 25 px rgba (255,192,203,0.7);
      text-align: center;
      transition: 0.5 s ease;
      z-index: 20;
    }
    .popup img {
      max-width: 300 px;
      border-radius: 12 px;
      box-shadow: 0 0 15 px rgba (255,182,193,0.8);
    }
    .popup.show {
      transform: translate (-50 %, -50 %) scale (1);
    }
    .popup button {
      margin-top: 10 px;
      background: #ff66b2;
      border: none;
      color: white;
      padding: 8 px 16 px;
      border-radius: 8 px;
      cursor: pointer;
      transition: 0.3 s;
    }
    .popup button:hover {
      background: #ff4da6;
    }
    /* Hoa rơi */
    .flower {
      position: absolute;
      width: 20 px;
      height: 20 px;
      background-image: url('https://cdn-icons-png.flaticon.com/512/616/616408.png');
      background-size: cover;
      opacity: 0.7;
      animation: fall linear infinite;
    }
    @keyframes fall {
      from { transform: translateY(-10vh) rotate (0deg); opacity: 1; }
      to { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }
    /* Sao lấp lánh */
    .star {
      position: absolute;
      width: 3 px;
      height: 3 px;
      background: white;
      border-radius: 50 %;
      animation: sparkle 2 s infinite ease-in-out;
      opacity: 0.8;
    }
    @keyframes sparkle {
      0 %, 100 % { opacity: 0.3; }
      50 % { opacity: 1; }
    }
  </style>
</head>
<body>
  <!-- Màn mở đầu -->
  <div class="intro" id="intro">
    <h2 id="startBtn">💌 Gửi Hoàng Trang 💌</h2>
  </div>
  <!-- Thiệp -->
  <div class="card" id="card">
    <h1>🎀 Chúc mừng sinh nhật 🎀</h1>
    <p>Chúc cậu một ngày sinh nhật thật ngọt ngào,<br>
    tràn đầy yêu thương và những điều dịu dàng nhất 💖<br>
    Hãy luôn rạng rỡ và hạnh phúc như ánh sao đêm nay nhé ✨</p>
  </div>
  <!-- Nút quà -->
  <button class="gift-btn" id="giftButton">
    <img src="https://cdn-icons-png.flaticon.com/512/869/869869.png" alt="Gift">
  </button>
  <!-- Hộp ảnh -->
  <div class="popup" id="popup">
    <img src="anh.jfif" alt="Ảnh quà sinh nhật">
    <br>
    <button onclick="closePopup()">Đóng 💗</button>
  </div>
  <!-- Nhạc -->
  <audio id="music" autoplay muted loop>
    <source src="https://archive.org/download/CanonInD_261/CanonInD.mp3" type="audio/mpeg">
  </audio>
  <script>
    const intro = document.getElementById('intro');
    const card = document.getElementById('card');
    const giftBtn = document.getElementById('giftButton');
    const music = document.getElementById('music');
    // Khi bấm "Gửi cậu"
    document.getElementById('startBtn').addEventListener('click', () => {
      intro.classList.add('hidden');
      card.classList.add('show');
      giftBtn.classList.add('show');
      setTimeout(() => {
        music.muted = false;
        music.volume = 0.8;
        music.play();
      }, 1000);
    });
    // Hoa rơi
    for (let i = 0; i < 20; i++) {
      const flower = document.createElement('div');
      flower.classList.add('flower');
      flower.style.left = Math.random() * 100 + 'vw';
      flower.style.animationDuration = 5 + Math.random() * 5 + 's';
      flower.style.animationDelay = Math.random() * 5 + 's';
      flower.style.transform = `scale(${0.8 + Math.random() * 0.5})`;
      document.body.appendChild(flower);
    }
    // Sao lấp lánh
    for (let i = 0; i < 30; i++) {  
      const star = document.createElement('div');
      star.classList.add('star');
      star.style.left = Math.random() * 100 + 'vw';
      star.style.top = Math.random() * 100 + 'vh';
      star.style.animationDelay = Math.random() * 2 + 's';
      document.body.appendChild(star);
    }
    // Nút quà mở ảnh
    const popup = document.getElementById('popup');
    giftBtn.addEventListener('click', () => {
      popup.classList.add('show');
    });
    function closePopup() {
      popup.classList.remove('show');
    }
  </script>

</body>
</html>
