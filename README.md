<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Important Question 💭</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }
    html, body {
      height: 100%;
      width: 100%;
      overflow: hidden;
    }
    body {
      min-height: 100dvh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
      padding: 20px;
    }
    .container {
      background: white;
      padding: clamp(24px, 6vw, 40px);
      border-radius: 20px;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
      text-align: center;
      width: 100%;
      max-width: 420px;
    }
    h1 {
      font-size: clamp(1.5rem, 6vw, 2rem);
      color: #333;
      margin-bottom: 10px;
    }
    .question {
      font-size: clamp(1.1rem, 5vw, 1.4rem);
      color: #c0392b;
      margin-bottom: 10px;
      font-weight: 600;
    }
    .subtext {
      font-size: clamp(0.85rem, 3.5vw, 0.95rem);
      color: #888;
      margin-bottom: 25px;
      font-style: italic;
    }
    .buttons {
      display: flex;
      gap: 16px;
      justify-content: center;
      flex-wrap: wrap;
      min-height: 80px;
      align-items: center;
      position: relative;
    }
    button {
      padding: 16px 36px;
      font-size: clamp(1rem, 4vw, 1.1rem);
      border: none;
      border-radius: 50px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-weight: 700;
      min-height: 54px;
      touch-action: manipulation;
      user-select: none;
      -webkit-user-select: none;
    }
    .yes-btn {
      background: linear-gradient(135deg, #c0392b 0%, #e74c3c 100%);
      color: white;
    }
    .yes-btn:active {
      transform: scale(1.05);
    }
    .no-btn {
      background: linear-gradient(135deg, #555 0%, #888 100%);
      color: white;
      position: relative;
      transition: all 0.3s ease;
    }
    .no-btn:active {
      transform: scale(0.95);
    }
    .no-response {
      color: #c0392b;
      font-size: clamp(0.85rem, 3.5vw, 1rem);
      margin-top: 15px;
      font-style: italic;
      min-height: 30px;
      font-weight: 600;
      line-height: 1.4;
    }
    .success-screen {
      display: none;
    }
    .success-screen .emoji-big {
      font-size: clamp(3rem, 12vw, 4rem);
      margin-bottom: 15px;
      animation: pulse 0.8s infinite;
      display: block;
    }
    .success-screen h2 {
      font-size: clamp(1.4rem, 6vw, 1.8rem);
      color: #c0392b;
      margin-bottom: 10px;
    }
    .success-screen p {
      font-size: clamp(0.95rem, 4vw, 1.1rem);
      color: #555;
      margin-top: 10px;
      line-height: 1.6;
    }
    .success-screen .spicy {
      font-size: clamp(0.85rem, 3.5vw, 1rem);
      color: #888;
      font-style: italic;
      margin-top: 15px;
    }
    .miss-too {
      margin-top: 15px;
      font-size: clamp(1rem, 4.5vw, 1.3rem);
      color: #c0392b;
      font-weight: 700;
      line-height: 1.5;
    }
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.15); }
    }
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-6px); }
      75% { transform: translateX(6px); }
    }
    .shake {
      animation: shake 0.3s ease;
    }
    .confetti {
      position: fixed;
      width: 10px;
      height: 10px;
      animation: fall 3s linear forwards;
      pointer-events: none;
      z-index: 999;
    }
    @keyframes fall {
      to {
        transform: translateY(110vh) rotate(720deg);
        opacity: 0;
      }
    }
    .progress-bar-wrap {
      margin-top: 20px;
      background: #eee;
      border-radius: 10px;
      height: 8px;
      overflow: hidden;
    }
    .progress-bar {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #c0392b, #e74c3c);
      border-radius: 10px;
      transition: width 0.4s ease;
    }
    .progress-label {
      font-size: 0.75rem;
      color: #aaa;
      margin-top: 5px;
    }
  </style>
</head>
<body>

  <div class="container" id="questionScreen">
    <h1>Oi, you 👀</h1>
    <p class="question">Do you miss me?</p>
    <p class="subtext">…and I mean <em>all</em> of me 😏</p>
    <div class="buttons">
      <button class="yes-btn" onclick="sayYes()">Obviously 🥵</button>
      <button class="no-btn" id="noBtn" onclick="sayNo()">No 🙄</button>
    </div>
    <p class="no-response" id="noResponse"></p>
    <div class="progress-bar-wrap" id="honestyWrap" style="display:none">
      <div class="progress-bar" id="honestyBar"></div>
      <p class="progress-label">Honesty level loading... 🌡️</p>
    </div>
  </div>

  <div class="container success-screen" id="successScreen">
    <span class="emoji-big">🔥</span>
    <h2>Thought so 😏</h2>
    <p>You lasted <span id="noCount">0</span> seconds of denial before admitting it.</p>
    <p class="miss-too">Good. Because I miss you too.<br>Every. Single. Part. 😈</p>
    <p class="spicy">Now stop playing hard to get and text me 📱💋</p>
  </div>

  <script>
    const noMessages = [
      "Sure babe, sure 😏",
      "Your body disagrees with you 🔥",
      "Stop lying to yourself, daddy 💀",
      "Not even a little? Not even that tight pussy? 👀",
      "Denial looks cute on you, not convincing 😂",
      "Your brain said no, your dick said otherwise 🫀",
      "You literally clicked this link though… 🤔",
      "Come on. You remember. Don't lie. 😈",
      "That's not what you were thinking last night 💭",
      "Still no? Bold choice 😂",
      "Your thumbs came here on their own? Right. 🙄",
      "The audacity is sending me 💀💀",
      "Fine, keep lying. The Yes button is right there 😏",
      "Your dreams already told on you 😴💭",
      "Last chance before this button disappears 🏃"
    ];

    let noClickCount = 0;
    let denialStart = null;

    const noBtn = document.getElementById('noBtn');
    const noResponse = document.getElementById('noResponse');
    const honestyWrap = document.getElementById('honestyWrap');
    const honestyBar = document.getElementById('honestyBar');

    function sayNo() {
      if (!denialStart) denialStart = Date.now();

      const msg = noMessages[Math.min(noClickCount, noMessages.length - 1)];
      noResponse.textContent = msg;
      noClickCount++;

      if (noClickCount === 2) honestyWrap.style.display = 'block';

      const pct = Math.min((noClickCount / noMessages.length) * 100, 100);
      honestyBar.style.width = pct + '%';

      noBtn.classList.add('shake');
      setTimeout(() => noBtn.classList.remove('shake'), 350);

      const size = Math.max(0.75, 1.1 - noClickCount * 0.03);
      noBtn.style.fontSize = size + 'rem';
      noBtn.style.padding = `${Math.max(10, 16 - noClickCount)}px ${Math.max(18, 36 - noClickCount * 2)}px`;

      if (noClickCount > 7) {
        const maxX = 70;
        const maxY = 30;
        const x = (Math.random() * maxX * 2 - maxX);
        const y = (Math.random() * maxY * 2 - maxY);
        noBtn.style.transform = `translate(${x}px, ${y}px)`;
      }

      if (noClickCount >= noMessages.length) {
        noBtn.style.opacity = '0';
        noBtn.style.pointerEvents = 'none';
        noResponse.textContent = "The No button left the chat. Just press Obviously. 😂";
      }
    }

    function sayYes() {
      const elapsed = denialStart ? Math.round((Date.now() - denialStart) / 1000) : 0;
      document.getElementById('noCount').textContent = elapsed;
      document.getElementById('questionScreen').style.display = 'none';
      document.getElementById('successScreen').style.display = 'block';
      createConfetti();
    }

    function createConfetti() {
      const colors = ['#c0392b', '#e74c3c', '#ff6b6b', '#ff9ff3', '#feca57', '#ff4757'];
      for (let i = 0; i < 60; i++) {
        setTimeout(() => {
          const el = document.createElement('div');
          el.className = 'confetti';
          el.style.left = Math.random() * 100 + 'vw';
          el.style.top = '-10px';
          el.style.background = colors[Math.floor(Math.random() * colors.length)];
          el.style.borderRadius = Math.random() > 0.5 ? '50%' : '2px';
          el.style.width = (Math.random() * 8 + 6) + 'px';
          el.style.height = (Math.random() * 8 + 6) + 'px';
          document.body.appendChild(el);
          setTimeout(() => el.remove(), 3500);
        }, i * 40);
      }
    }
  </script>
</body>
</html>
