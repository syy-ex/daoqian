<html lang="zh-CN"><head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>给老师的一封道歉信</title>
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --accent:#7c3aed; --glass: rgba(255,255,255,0.04);
      --text:#e6eef8; --muted:#b7c2d6;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;font-family:Inter, system-ui, "Segoe UI", Roboto, 'Hiragino Sans GB', 'PingFang SC', 'Microsoft Yahei', sans-serif;
      background: radial-gradient(1200px 500px at 10% 10%, rgba(124,58,237,0.12), transparent),
                  radial-gradient(900px 400px at 90% 90%, rgba(59,130,246,0.06), transparent),
                  var(--bg);
      color:var(--text); -webkit-font-smoothing:antialiased;
      padding:36px; display:flex; align-items:center; justify-content:center;
    }

    .wrap{width:100%;max-width:960px}

    header{display:flex;align-items:center;gap:16px;margin-bottom:18px}
    .logo{width:72px;height:72px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#2563eb);display:flex;align-items:center;justify-content:center;box-shadow:0 8px 30px rgba(2,6,23,0.6)}
    .logo strong{font-size:20px}

    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:16px; padding:28px; box-shadow: 0 10px 40px rgba(2,6,23,0.6); backdrop-filter: blur(8px); border:1px solid rgba(255,255,255,0.04)}

    .grid{display:grid;grid-template-columns:1fr;gap:20px;align-items:start}
    @media (max-width:900px){ .grid{grid-template-columns:1fr} }

    /* Letter area */
    .letter{padding:20px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.012), transparent);min-height:420px;position:relative}

    .meta{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
    .meta .fromto{font-size:14px;color:var(--muted)}

    .content{font-size:18px;line-height:1.65;color:var(--text);white-space:pre-wrap}

    .controls{display:flex;gap:10px;margin-top:16px}
    button{background:var(--accent);border:0;padding:10px 14px;border-radius:10px;color:white;font-weight:600;cursor:pointer}
    .ghost{background:transparent;border:1px solid rgba(255,255,255,0.06)}

    /* Canvas handwriting */
    .sig-wrap{margin-top:18px;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent);padding:10px;border-radius:10px}
    canvas#handwriting{width:100%;height:300px;border-radius:8px;background:linear-gradient(90deg, rgba(255,255,255,0.02), transparent);display:block}
    .hint{font-size:13px;color:var(--muted);margin-top:8px}

    /* Sidebar */
    .sidebar{padding:18px;border-radius:12px;background:linear-gradient(90deg, rgba(255,255,255,0.02), transparent)}
    .sidebar h3{margin:0 0 8px 0}
    .field{margin-bottom:12px}
    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type=text],textarea,select{width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:var(--text)}

    /* small tech demo indicators */
    .tech-list{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
    .chip{padding:6px 10px;border-radius:999px;background:var(--glass);font-size:13px;color:var(--muted);border:1px solid rgba(255,255,255,0.02)}

    footer{margin-top:14px;color:var(--muted);font-size:13px}

    /* accessibility: motion reduce */
    @media (prefers-reduced-motion: reduce){ *{transition:none!important;animation:none!important} }

  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo" aria-hidden="true"><strong>道</strong></div>
      <div>
        <h1 style="margin:0;font-size:20px">致老师的一封道歉信</h1>
      </div>
    </header>

    <main class="card" role="main">
      <div class="grid">
        <section class="letter" aria-label="道歉信预览">
          <div class="meta">
            <div class="fromto">发件人：朱同学 &nbsp;→&nbsp; 收件人：刘老师</div>
            <div id="date" class="fromto">2025/11/4 </div>
          </div>

          <div id="preview" class="content" tabindex="0" role="article" aria-live="polite">
        <!-- 默认内容会在JS中填充 -->
      </div>

          <div class="sig-wrap" aria-hidden="false">
            <div style="margin-bottom:8px; color:var(--muted); font-size:14px;">手写区域（使用鼠标或触摸书写）</div>
            <canvas id="handwriting" width="800" height="300"></canvas>
          </div>

          <div class="controls">
            <button id="speakBtn">朗读这封信</button>
          </div>


        </section>
      </div>
    </main>
  </div>

  <script>
    // 小工具：日期
    document.getElementById('date').textContent = new Date().toLocaleDateString();

    // 默认模板生成器
    function makeMessage(student, teacher, reason, tone){
      const base = `尊敬的${teacher}：\n\n首先我想对您说一声真诚的抱歉。\n我在最近的课程中旷课，这样的行为是错误的，给您带来了不便和困扰，我深感愧疚。`;
      const extra = reason? (`\n\n关于原因：${reason}。我知道这不是不是借口，但我希望您能理解我当时的处境。`) : '';
      let closing = '';
      if(tone === 'formal') closing = `\n\n请您尽管批评教育，我一定会认真反省。\n此致\n敬礼\n\n${student}`;
      else if(tone === 'simple') closing = `\n\n抱歉，我会改正，请老师批评。\n\n${student}`;
      else closing = `\n\n我非常后悔这次的行为，请老师严肃批评，我会用实际行动证明我的改变。\n\n${student}`;
      return base + extra + closing;
    }

    const preview = document.getElementById('preview');

    // 使用默认值渲染
    function render(){
      const text = makeMessage('学生', '老师', '', 'formal');
      preview.textContent = text;
    }
    // initial
    render();

    // SpeechSynthesis
    const speakBtn = document.getElementById('speakBtn');
    function speak(){
      if(!('speechSynthesis' in window)) { alert('此浏览器不支持 SpeechSynthesis'); return; }
      const u = new SpeechSynthesisUtterance(preview.textContent);
      u.lang = 'zh-CN'; u.rate = 0.95; u.pitch = 1;
      speechSynthesis.cancel(); speechSynthesis.speak(u);
    }
    speakBtn.addEventListener('click', speak);



    // handwriting canvas
    const canvas = document.getElementById('handwriting');
    const ctx = canvas.getContext('2d');
    let drawing=false; let last={x:0,y:0}; let drawingDataURL=null;

    // hi-dpi scaling
    function scaleCanvas(){
      const ratio = window.devicePixelRatio||1;
      const w = canvas.clientWidth; const h = canvas.clientHeight;
      canvas.width = Math.floor(w*ratio); canvas.height = Math.floor(h*ratio);
      canvas.style.width = w+'px'; canvas.style.height = h+'px';
      ctx.scale(ratio, ratio);
      redrawBackground();
    }
    function redrawBackground(){
      ctx.clearRect(0,0,canvas.width,canvas.height);
      // subtle ruled lines
      const h = canvas.clientHeight; const w = canvas.clientWidth;
      ctx.save(); ctx.globalAlpha=0.06; ctx.strokeStyle='#fff'; ctx.lineWidth=1;
      for(let y=20;y<h;y+=20){ ctx.beginPath(); ctx.moveTo(10,y); ctx.lineTo(w-10,y); ctx.stroke(); }
      ctx.restore();
      // if there's a saved drawing, keep it
      if(drawingDataURL){ const img = new Image(); img.onload = ()=>{ ctx.drawImage(img,0,0,w,h); }; img.src = drawingDataURL; }
    }
    window.addEventListener('resize', ()=>{ scaleCanvas(); }); scaleCanvas();

    function posFromEvent(e){ const rect = canvas.getBoundingClientRect(); const touch = e.touches && e.touches[0]; const clientX = touch? touch.clientX : e.clientX; const clientY = touch? touch.clientY : e.clientY; return {x:clientX-rect.left, y:clientY-rect.top}; }

    canvas.addEventListener('pointerdown', (e)=>{ drawing=true; last = posFromEvent(e); canvas.setPointerCapture(e.pointerId); });
    canvas.addEventListener('pointermove', (e)=>{ if(!drawing) return; const p = posFromEvent(e); stroke(last.x,last.y,p.x,p.y); last = p; });
    canvas.addEventListener('pointerup', (e)=>{ drawing=false; drawingDataURL = canvas.toDataURL('image/png'); });
    canvas.addEventListener('pointerleave', ()=>{ drawing=false; });

    function stroke(x1,y1,x2,y2){ ctx.save(); ctx.lineCap='round'; ctx.lineJoin='round'; ctx.strokeStyle='rgba(255,255,255,0.95)'; ctx.lineWidth=2.6; ctx.beginPath(); ctx.moveTo(x1,y1); ctx.lineTo(x2,y2); ctx.stroke(); ctx.restore(); }



    // 绘制"朱海宁"三个字
    function drawZhuHaiNing() {
      ctx.save();
      ctx.font = 'bold 48px "Microsoft YaHei", sans-serif';
      ctx.fillStyle = 'rgba(255, 255, 255, 0.95)';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('朱海宁', canvas.width / 2, canvas.height / 2);
      ctx.restore();
      drawingDataURL = canvas.toDataURL('image/png');
    }
    
    // 页面加载完成后自动绘制签名
    window.addEventListener('load', () => {
      setTimeout(drawZhuHaiNing, 500);
    });

    // Helper: expose speak for keyboard
    window.speak = speak;

    // Ensure preview is focusable and announced
    preview.addEventListener('focus', ()=>{ preview.setAttribute('aria-label','道歉信预览，按朗读按钮可读出'); });

    // End of script
  </script>



</body></html>
