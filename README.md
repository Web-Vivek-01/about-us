<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Redeem Your Web Dev Power-Up!</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background: linear-gradient(135deg, #667eea, #764ba2, #ff6a00);
      min-height: 100vh;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0;
    }
    .redeem-container {
      background: rgba(255,255,255,0.95);
      border-radius: 18px;
      box-shadow: 0 8px 32px 0 rgba(31,38,135,0.37);
      padding: 40px 32px;
      max-width: 350px;
      width: 100%;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .redeem-title {
      font-size: 1.8em;
      font-weight: bold;
      color: #4f3dbb;
      margin-bottom: 8px;
      letter-spacing: 1px;
    }
    .redeem-subtitle {
      color: #666;
      font-size: 1.1em;
      margin-bottom: 20px;
    }
    .redeem-btn {
      background: linear-gradient(90deg, #ffb347 0%, #ff6a00 100%);
      color: #fff;
      border: none;
      border-radius: 8px;
      padding: 14px 38px;
      font-size: 1.1em;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.2s;
      margin-bottom: 10px;
      box-shadow: 0 4px 16px 0 rgba(255,106,0,0.2);
    }
    .redeem-btn:active {
      background: linear-gradient(90deg, #ff6a00 0%, #ffb347 100%);
    }
    .code-box {
      background: #f7f7fa;
      color: #333;
      border-radius: 8px;
      font-size: 1.3em;
      padding: 14px;
      margin-top: 18px;
      letter-spacing: 2px;
      border: 2px dashed #764ba2;
      display: none;
      animation: pop 0.5s;
    }
    @keyframes pop {
      0% { transform: scale(0.7); opacity: 0.2;}
      70% { transform: scale(1.1);}
      100% { transform: scale(1); opacity: 1;}
    }
    .confetti {
      position: absolute;
      left: 0; top: 0; width: 100%; height: 100%;
      pointer-events: none;
      z-index: 10;
    }
  </style>
</head>
<body>
  <div class="redeem-container">
    <canvas class="confetti"></canvas>
    <div class="redeem-title">🎉 Redeem Your Code!</div>
    <div class="redeem-subtitle">Unlock your web dev power-up below</div>
    <button class="redeem-btn" id="redeemBtn">Redeem Now</button>
    <div class="code-box" id="codeBox">WEBDEV-POWER-UP-2025</div>
  </div>
  <script>
    const btn = document.getElementById('redeemBtn');
    const codeBox = document.getElementById('codeBox');
    btn.addEventListener('click', function() {
      codeBox.style.display = 'block';
      btn.disabled = true;
      btn.textContent = 'Redeemed!';
      launchConfetti();
    });

    // Simple confetti animation
    function launchConfetti() {
      const canvas = document.querySelector('.confetti');
      const ctx = canvas.getContext('2d');
      canvas.width = canvas.offsetWidth;
      canvas.height = canvas.offsetHeight;
      let confetti = [];
      for (let i = 0; i < 40; i++) {
        confetti.push({
          x: Math.random() * canvas.width,
          y: -10,
          r: 6 + Math.random() * 8,
          d: Math.random() * 40,
          color: `hsl(${Math.random()*360}, 70%, 60%)`,
          tilt: Math.random() * 10 - 10
        });
      }
      let angle = 0;
      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        angle += 0.01;
        for (let i = 0; i < confetti.length; i++) {
          let c = confetti[i];
          c.y += Math.cos(angle + c.d) + 2 + c.r/4;
          c.x += Math.sin(angle) * 2;
          c.tilt += Math.random() * 0.8 - 0.4;
          ctx.beginPath();
          ctx.arc(c.x + c.tilt, c.y, c.r, 0, Math.PI * 2, false);
          ctx.fillStyle = c.color;
          ctx.fill();
        }
      }
      function update() {
        draw();
        confetti.forEach(c => {
          if (c.y > canvas.height + 10) {
            c.x = Math.random() * canvas.width;
            c.y = -10;
          }
        });
        requestAnimationFrame(update);
      }
      update();
      setTimeout(() => { ctx.clearRect(0, 0, canvas.width, canvas.height); }, 3000);
    }
  </script>
</body>
</html>
