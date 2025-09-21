<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simulador AUTOPS – Polarizado Profesional</title>
  <style>
    body{margin:0;font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;background:linear-gradient(135deg,#1a1a2e 0%,#16213e 50%,#0f3460 100%);color:#fff;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;padding:20px}
    
    .header{text-align:center;margin-bottom:30px}
    .logo{font-size:2.8rem;font-weight:900;letter-spacing:2px;margin-bottom:8px;display:inline-block}
    .logo .a{color:#22c55e;text-shadow:0 0 15px rgba(34,197,94,0.4)}
    .logo .u{color:#fbbf24;text-shadow:0 0 15px rgba(251,191,36,0.4)}
    .logo .t{color:#ef4444;text-shadow:0 0 15px rgba(239,68,68,0.4)}
    .logo .o{color:#3b82f6;text-shadow:0 0 15px rgba(59,130,246,0.4)}
    .logo .p{color:#22c55e;text-shadow:0 0 15px rgba(34,197,94,0.4)}
    .logo .s{color:#fbbf24;text-shadow:0 0 15px rgba(251,191,36,0.4)}
    .logo .com{color:#6b7280;font-size:1.8rem;text-shadow:0 0 10px rgba(107,114,128,0.3)}
    .slogan{background:linear-gradient(90deg,#22c55e,#fbbf24,#ef4444,#3b82f6);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;font-style:italic;font-size:1.1rem;margin-bottom:8px;font-weight:600}
    .tagline{color:#ccc;font-size:0.9rem;opacity:0.8}
    
    .stage{position:relative;width:85%;max-width:900px;aspect-ratio:16/9;border:3px solid;border-image:linear-gradient(45deg,#22c55e,#fbbf24,#ef4444,#3b82f6) 1;border-radius:15px;overflow:hidden;display:grid;place-items:center;margin-bottom:25px;background:rgba(255,255,255,0.95);box-shadow:0 10px 30px rgba(34,197,94,0.2);touch-action:none}
    
    canvas{width:100%;height:100%;touch-action:none}
    
    .upload-area{color:#333;font-size:1.1rem;cursor:pointer;text-align:center;padding:40px;border-radius:10px;background:linear-gradient(45deg,#f8f9fa,#e9ecef);border:2px dashed;border-image:linear-gradient(45deg,#22c55e,#fbbf24,#ef4444,#3b82f6) 1;transition:all 0.3s ease}
    .upload-area:hover{background:linear-gradient(45deg,#e9ecef,#f8f9fa);transform:scale(1.02)}
    
    .controls{width:85%;max-width:900px;display:flex;flex-direction:column;gap:15px;background:rgba(255,255,255,0.1);padding:25px;border-radius:15px;backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,0.2)}
    
    .controls button{padding:12px 18px;border:none;border-radius:10px;font-weight:600;cursor:pointer;font-size:1rem;transition:all 0.3s ease;text-transform:uppercase;letter-spacing:1px}
    .controls button:hover{transform:translateY(-2px);box-shadow:0 5px 15px rgba(0,0,0,0.3)}
    
    .btn-primary{background:linear-gradient(135deg,#22c55e,#16a34a);color:#fff;border:2px solid transparent}
    .btn-primary:hover{background:linear-gradient(135deg,#16a34a,#22c55e)}
    
    .btn-success{background:linear-gradient(135deg,#fbbf24,#f59e0b);color:#fff;border:2px solid transparent}
    .btn-success:hover{background:linear-gradient(135deg,#f59e0b,#fbbf24)}
    
    .btn-warning{background:linear-gradient(135deg,#ef4444,#dc2626);color:#fff;border:2px solid transparent}
    .btn-warning:hover{background:linear-gradient(135deg,#dc2626,#ef4444)}
    
    .btn-info{background:linear-gradient(135deg,#3b82f6,#2563eb);color:#fff;border:2px solid transparent}
    .btn-info:hover{background:linear-gradient(135deg,#2563eb,#3b82f6)}
    
    .button-group{display:flex;gap:10px;flex-wrap:wrap;justify-content:center}
    
    .group{margin-bottom:15px;background:rgba(255,255,255,0.1);padding:15px;border-radius:10px}
    .label{display:flex;justify-content:space-between;font-size:1rem;margin-bottom:8px;color:#fff;font-weight:500}
    .label .percentage{background:linear-gradient(90deg,#22c55e,#fbbf24,#ef4444,#3b82f6);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;font-weight:700;font-size:1.1rem}
    
    input[type=range]{width:100%;height:8px;border-radius:5px;background:rgba(255,255,255,0.3);outline:none;appearance:none}
    input[type=range]::-webkit-slider-thumb{appearance:none;width:20px;height:20px;border-radius:50%;background:linear-gradient(135deg,#22c55e,#fbbf24,#ef4444,#3b82f6);cursor:pointer;box-shadow:0 2px 10px rgba(34,197,94,0.5)}
    input[type=range]::-moz-range-thumb{width:20px;height:20px;border-radius:50%;background:linear-gradient(135deg,#22c55e,#fbbf24,#ef4444,#3b82f6);cursor:pointer;border:none;box-shadow:0 2px 10px rgba(34,197,94,0.5)}
    
    .zoom-info{text-align:center;margin-bottom:15px;padding:10px;background:rgba(34,197,94,0.2);border-radius:8px;font-size:0.9rem;color:#22c55e}
    
    .footer{margin-top:30px;text-align:center;color:#ccc;font-size:0.9rem}
    .footer a{background:linear-gradient(90deg,#22c55e,#fbbf24,#ef4444,#3b82f6);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;text-decoration:none;font-weight:600}
    .footer a:hover{transform:scale(1.05)}
    
    @media (max-width: 768px) {
      .logo{font-size:2rem}
      .logo .com{font-size:1.4rem}
      .slogan{font-size:1rem}
      .tagline{font-size:0.8rem}
      .stage{width:95%;margin-bottom:20px}
      .controls{width:95%;padding:20px}
      .button-group{flex-direction:column;gap:15px}
      .controls button{width:100%;padding:15px 18px;font-size:1.1rem}
      .upload-area{padding:30px;font-size:1rem}
      .group{padding:12px;margin-bottom:12px}
      .label{font-size:0.9rem}
      .label .percentage{font-size:1rem}
      input[type=range]{height:10px}
      input[type=range]::-webkit-slider-thumb{width:24px;height:24px}
      input[type=range]::-moz-range-thumb{width:24px;height:24px}
      body{padding:15px}
      .footer{margin-top:20px;font-size:0.8rem}
      .zoom-info{font-size:0.8rem;padding:8px}
    }
    
    @media (max-width: 480px) {
      .logo{font-size:1.8rem}
      .logo .com{font-size:1.2rem}
      .slogan{font-size:0.9rem}
      .stage{width:98%}
      .controls{width:98%;padding:15px}
      .controls button{padding:12px 15px;font-size:1rem}
      .upload-area{padding:25px;font-size:0.9rem}
      .group{padding:10px}
      body{padding:10px}
    }
    
    /* Mejoras para touch en móviles */
    .controls button{
      touch-action:manipulation;
      -webkit-tap-highlight-color:transparent;
    }
    
    input[type=range]{
      touch-action:pan-x;
    }
    
    /* Prevenir zoom en inputs */
    input[type=file]{
      font-size:16px;
    }
  </style>
</head>
<body>
  <div class="header">
    <div class="logo">
      <span class="a">A</span><span class="u">U</span><span class="t">T</span><span class="o">O</span><span class="p">P</span><span class="s">S</span><span class="com">.com</span>
    </div>
    <div class="slogan">"Calidad y Confianza Morelia"</div>
    <div class="tagline">Simulador Profesional de Polarizado</div>
  </div>

  <div class="stage" id="stage">
    <label id="uploadArea" class="upload-area">
      <div><strong>📸 Haz clic para subir una foto de tu vehículo</strong></div>
      <div style="font-size:0.9rem;margin-top:8px;opacity:0.7">Formatos: JPG, PNG, GIF</div>
      <input id="fileInput" type="file" accept="image/*" style="display:none" />
    </label>
    <canvas id="canvas" width="1280" height="720" style="display:none"></canvas>
  </div>

  <div class="controls">
    <div id="zoomInfo" class="zoom-info" style="display:none">
      📱 <strong>Móvil:</strong> Pellizca para zoom • Arrastra para mover • <strong>Toca SIN mover</strong> para seleccionar puntos
    </div>
    <div class="button-group">
      <button class="btn-primary" id="btnSelect">🎯 Seleccionar Cristal</button>
      <button class="btn-success" id="btnFinish" style="display:none">✅ Terminar Selección</button>
      <button class="btn-warning" id="btnAdd" style="display:none">➕ Agregar Cristal</button>
      <button class="btn-info" id="btnReset" style="display:none">🔄 Reiniciar Zoom</button>
    </div>
    <div id="sliders"></div>
  </div>

  <div class="footer">
    <p>Desarrollado por <a href="https://autops.com">AUTOPS.COM</a> | Morelia, Michoacán</p>
    <p>Especialistas en autos usados y seminuevos premium</p>
  </div>

  <script>
    const MAX_PANES = 3;
    let imageDataURL = null;
    let drawing = false;
    let currentPolygon = [];
    let panes = [];

    // Variables para zoom y pan
    let scale = 1;
    let offsetX = 0;
    let offsetY = 0;
    let isPanning = false;
    let lastTouchDistance = 0;
    let isTouchDevice = false;

    // Variables para detectar movimiento vs tap
    let touchStartTime = 0;
    let touchMoved = false;
    let lastTouchX = 0;
    let lastTouchY = 0;
    let touchStartX = 0;
    let touchStartY = 0;

    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const stage = document.getElementById('stage');
    const uploadArea = document.getElementById('uploadArea');
    const fileInput = document.getElementById('fileInput');
    const zoomInfo = document.getElementById('zoomInfo');

    const btnSelect = document.getElementById('btnSelect');
    const btnFinish = document.getElementById('btnFinish');
    const btnAdd = document.getElementById('btnAdd');
    const btnReset = document.getElementById('btnReset');
    const slidersWrap = document.getElementById('sliders');

    // Detectar dispositivo móvil
    function detectTouch() {
      isTouchDevice = ('ontouchstart' in window) || (navigator.maxTouchPoints > 0);
      if (isTouchDevice) {
        zoomInfo.style.display = 'block';
      }
    }

    function loadImageToCanvas(src){
      const img = new Image();
      img.onload = () => {
        // Resetear zoom al cargar nueva imagen
        scale = 1;
        offsetX = 0;
        offsetY = 0;
        
        drawImageWithTransform(img);
        btnReset.style.display = 'inline-block';
      };
      img.src = src;
    }

    function drawImageWithTransform(img) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      
      // Calcular tamaño y posición base
      const sw = img.width, sh = img.height;
      const dw = canvas.width, dh = canvas.height;
      const baseScale = Math.min(dw/sw, dh/sh) * 1.25;
      const baseW = sw * baseScale, baseH = sh * baseScale;
      const baseX = (dw - baseW) / 2, baseY = (dh - baseH) / 2;
      
      // Aplicar transformaciones con offset
      ctx.save();
      ctx.translate(dw/2, dh/2); // Mover al centro del canvas
      ctx.translate(offsetX, offsetY); // Aplicar desplazamiento
      ctx.scale(scale, scale); // Aplicar zoom
      ctx.translate(-dw/2, -dh/2); // Volver al origen
      ctx.drawImage(img, 0, 0, sw, sh, baseX, baseY, baseW, baseH);
      ctx.restore();
      
      drawAllPanes();
    }

    function drawAllPanes(){
      if(!imageDataURL) return;
      const base = new Image();
      base.onload = () => {
        drawImageWithTransform(base);

        // Dibujar cristales con transformaciones
        ctx.save();
        ctx.translate(canvas.width/2, canvas.height/2); // Mover al centro
        ctx.translate(offsetX, offsetY); // Aplicar desplazamiento
        ctx.scale(scale, scale); // Aplicar zoom
        ctx.translate(-canvas.width/2, -canvas.height/2); // Volver al origen
        
        panes.forEach(p => {
          if(p.points.length > 2){
            ctx.beginPath();
            ctx.moveTo(p.points[0].x, p.points[0].y);
            for(let i=1;i<p.points.length;i++) ctx.lineTo(p.points[i].x, p.points[i].y);
            ctx.closePath();
            const alpha = 1 - (p.tint/100);
            ctx.fillStyle = `rgba(0,0,0,${alpha.toFixed(2)})`;
            ctx.fill();
          }
        });

        // Dibujar polígono actual
        if(currentPolygon.length){
          ctx.beginPath();
          ctx.moveTo(currentPolygon[0].x, currentPolygon[0].y);
          for(let i=1;i<currentPolygon.length;i++) ctx.lineTo(currentPolygon[i].x, currentPolygon[i].y);
          ctx.strokeStyle = '#22c55e';
          ctx.lineWidth = 3 / scale; // Ajustar grosor según zoom
          ctx.stroke();
          currentPolygon.forEach(p=>{
            ctx.beginPath();
            ctx.arc(p.x, p.y, 4 / scale, 0, Math.PI * 2); // Ajustar radio según zoom
            ctx.fillStyle = '#ef4444';
            ctx.fill();
            ctx.strokeStyle = '#22c55e';
            ctx.lineWidth = 2 / scale;
            ctx.stroke();
          });
        }
        
        ctx.restore();
      };
      base.src = imageDataURL;
    }

    function getCanvasScale(){
      const rect = canvas.getBoundingClientRect();
      return { sx: canvas.width/rect.width, sy: canvas.height/rect.height, rect };
    }

    function getTouchDistance(touches) {
      const dx = touches[0].clientX - touches[1].clientX;
      const dy = touches[0].clientY - touches[1].clientY;
      return Math.sqrt(dx * dx + dy * dy);
    }

    function getTouchCenter(touches) {
      return {
        x: (touches[0].clientX + touches[1].clientX) / 2,
        y: (touches[0].clientY + touches[1].clientY) / 2
      };
    }

    // Event listeners para zoom y pan
    canvas.addEventListener('touchstart', (e) => {
      e.preventDefault();
      if (!imageDataURL) return;
      
      touchStartTime = Date.now();
      touchMoved = false;
      
      if (e.touches.length === 2) {
        // Zoom con dos dedos
        lastTouchDistance = getTouchDistance(e.touches);
        isPanning = false;
      } else if (e.touches.length === 1) {
        // Preparar para pan con un dedo
        const { sx, sy, rect } = getCanvasScale();
        const touch = e.touches[0];
        lastTouchX = (touch.clientX - rect.left) * sx;
        lastTouchY = (touch.clientY - rect.top) * sy;
        
        // Guardar posición inicial para detectar movimiento
        touchStartX = lastTouchX;
        touchStartY = lastTouchY;
      }
    });

    canvas.addEventListener('touchmove', (e) => {
      e.preventDefault();
      if (!imageDataURL) return;
      
      if (e.touches.length === 2) {
        // Zoom
        const newDistance = getTouchDistance(e.touches);
        const scaleChange = newDistance / lastTouchDistance;
        const newScale = Math.max(0.5, Math.min(5, scale * scaleChange));
        
        if (newScale !== scale) {
          const center = getTouchCenter(e.touches);
          const { sx, sy, rect } = getCanvasScale();
          const centerX = (center.x - rect.left) * sx;
          const centerY = (center.y - rect.top) * sy;
          
          // Ajustar offset para zoom desde el centro de los dedos
          const oldScale = scale;
          scale = newScale;
          // Ajustar offset para mantener el punto de zoom centrado
          const zoomFactorChange = newScale / oldScale;
          offsetX = offsetX * zoomFactorChange + (centerX - canvas.width/2) * (zoomFactorChange - 1);
          offsetY = offsetY * zoomFactorChange + (centerY - canvas.height/2) * (zoomFactorChange - 1);
          
          drawAllPanes();
        }
        
        lastTouchDistance = newDistance;
        touchMoved = true; // Marcar como movimiento para evitar selección accidental
      } else if (e.touches.length === 1) {
        // Detectar si realmente se está moviendo (más de 10 píxeles)
        const { sx, sy, rect } = getCanvasScale();
        const touch = e.touches[0];
        const touchX = (touch.clientX - rect.left) * sx;
        const touchY = (touch.clientY - rect.top) * sy;
        
        const moveDistance = Math.sqrt(
          Math.pow(touchX - touchStartX, 2) + Math.pow(touchY - touchStartY, 2)
        );
        
        // Solo marcar como movimiento si se movió más de 10 píxeles
        if (moveDistance > 10) {
          touchMoved = true;
          
          // Pan con un dedo - mover la imagen
          const deltaX = touchX - lastTouchX;
          const deltaY = touchY - lastTouchY;
          
          offsetX += deltaX;
          offsetY += deltaY;
          
          drawAllPanes();
        }
        
        lastTouchX = touchX;
        lastTouchY = touchY;
      }
    });

    canvas.addEventListener('touchend', (e) => {
      if (!imageDataURL) return;
      
      // Solo procesar tap si no hubo movimiento significativo y fue un toque rápido
      if (e.touches.length === 0 && !touchMoved && Date.now() - touchStartTime < 500) {
        // Solo agregar punto si estamos en modo dibujo
        if (drawing && e.changedTouches.length === 1) {
          handleCanvasInteraction(e);
        }
      }
      
      if (e.touches.length === 0) {
        isPanning = false;
        touchMoved = false;
      }
    });

    // Zoom con rueda del mouse (desktop)
    canvas.addEventListener('wheel', (e) => {
      if (!imageDataURL) return;
      e.preventDefault();
      
      const scaleChange = e.deltaY > 0 ? 0.9 : 1.1;
      const newScale = Math.max(0.5, Math.min(5, scale * scaleChange));
      
      if (newScale !== scale) {
        const { sx, sy, rect } = getCanvasScale();
        const mouseX = (e.clientX - rect.left) * sx;
        const mouseY = (e.clientY - rect.top) * sy;
        
        const oldScale = scale;
        scale = newScale;
        // Ajustar offset para mantener el zoom centrado en el cursor
        const zoomFactorChange = newScale / oldScale;
        offsetX = offsetX * zoomFactorChange + (mouseX - canvas.width/2) * (zoomFactorChange - 1);
        offsetY = offsetY * zoomFactorChange + (mouseY - canvas.height/2) * (zoomFactorChange - 1);
        
        drawAllPanes();
      }
    });

    fileInput.addEventListener('change', (e)=>{
      const file = e.target.files && e.target.files[0];
      if(!file) return;
      
      uploadArea.innerHTML = '<div style="color:#666;">📱 Cargando imagen...</div>';
      
      const reader = new FileReader();
      reader.onload = (ev)=>{
        imageDataURL = ev.target.result;
        uploadArea.style.display = 'none';
        canvas.style.display = 'block';
        loadImageToCanvas(imageDataURL);
      }
      reader.readAsDataURL(file);
    });

    canvas.addEventListener('click', handleCanvasInteraction);

    function handleCanvasInteraction(e) {
      if(!drawing) return;
      e.preventDefault();
      
      const { sx, sy, rect } = getCanvasScale();
      let clientX, clientY;
      
      if(e.type === 'touchend' && e.changedTouches) {
        clientX = e.changedTouches[0].clientX;
        clientY = e.changedTouches[0].clientY;
      } else {
        clientX = e.clientX;
        clientY = e.clientY;
      }
      
      // Convertir coordenadas considerando zoom y pan
      const canvasX = (clientX - rect.left) * sx;
      const canvasY = (clientY - rect.top) * sy;
      
      // Ajustar por transformaciones (invertir las transformaciones)
      const centerX = canvas.width / 2;
      const centerY = canvas.height / 2;
      const transformedX = ((canvasX - centerX - offsetX) / scale) + centerX;
      const transformedY = ((canvasY - centerY - offsetY) / scale) + centerY;
      
      currentPolygon.push({x: transformedX, y: transformedY});
      drawAllPanes();
    }

    btnSelect.addEventListener('click', ()=>{
      if(!imageDataURL) { 
        if(window.innerWidth <= 768) {
          uploadArea.innerHTML = '<div><strong>📱 Toca para seleccionar imagen</strong></div><div style="font-size:0.8rem;margin-top:8px;opacity:0.7">Desde galería o cámara</div>';
        }
        fileInput.click(); 
        return; 
      }
      if(panes.length >= MAX_PANES){
        alert('🚫 Límite de 3 cristales alcanzado.\n\nPuedes ajustar la intensidad del polarizado de los cristales ya seleccionados.');
        return;
      }
      drawing = true;
      currentPolygon = [];
      btnFinish.style.display = 'inline-block';
      btnAdd.style.display = 'none';
      btnSelect.textContent = '📱 Toca en el cristal...';
    });

    btnFinish.addEventListener('click', ()=>{
      if(currentPolygon.length > 2){
        const closed = currentPolygon.concat([currentPolygon[0]]);
        panes.push({ points: closed, tint: 100 });
        renderSliders();
      }
      drawing = false;
      currentPolygon = [];
      btnFinish.style.display = 'none';
      btnSelect.textContent = '🎯 Seleccionar Cristal';
      if(panes.length < MAX_PANES) btnAdd.style.display = 'inline-block';
      drawAllPanes();
    });

    btnAdd.addEventListener('click', ()=>{
      if(panes.length >= MAX_PANES){
        btnAdd.style.display = 'none';
        return;
      }
      drawing = true;
      currentPolygon = [];
      btnFinish.style.display = 'inline-block';
      btnAdd.style.display = 'none';
    });

    btnReset.addEventListener('click', ()=>{
      scale = 1;
      offsetX = 0;
      offsetY = 0;
      drawAllPanes();
    });

    function renderSliders(){
      slidersWrap.innerHTML = '';
      panes.forEach((pane, idx)=>{
        const group = document.createElement('div');
        group.className = 'group';

        const label = document.createElement('div');
        label.className = 'label';
        label.innerHTML = `<span>🚗 Cristal ${idx+1}</span><span class="percentage">${100 - pane.tint}% Polarizado</span>`;

        const input = document.createElement('input');
        input.type = 'range';
        input.min = '0';
        input.max = '100';
        input.step = '1';
        input.value = String(pane.tint);
        input.addEventListener('input', (ev)=>{
          const val = Number(ev.target.value);
          panes[idx].tint = val;
          label.innerHTML = `<span>🚗 Cristal ${idx+1}</span><span class="percentage">${100 - val}% Polarizado</span>`;
          drawAllPanes();
        });

        group.appendChild(label);
        group.appendChild(input);
        slidersWrap.appendChild(group);
      });
      
      if(panes.length < MAX_PANES) {
        btnAdd.style.display = 'inline-block';
      } else {
        btnAdd.style.display = 'none';
      }
    }

    // Inicializar
    detectTouch();

    // Efecto de brillo dinámico en las letras del logo
    const logoLetters = document.querySelectorAll('.logo span');
    const colors = ['#22c55e', '#fbbf24', '#ef4444', '#3b82f6'];
    
    setInterval(() => {
      logoLetters.forEach((letter, index) => {
        const intensity = 10 + Math.random() * 15;
        const opacity = 0.3 + Math.random() * 0.4;
        if(index < 6) {
          const colorIndex = index % colors.length;
          letter.style.textShadow = `0 0 ${intensity}px ${colors[colorIndex]}${Math.floor(opacity * 255).toString(16).padStart(2, '0')}`;
        }
      });
    }, 1500);

  </script>
</body>
</html>
