# proyecto-
tiempo<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title> Organiza tu tiempo</title>
  <style>
    :root{
      --bg:#f8fafc; --card:#ffffff; --muted:#6b7280; --accent1:#fb7185; --accent2:#f97316;
      --glass: rgba(255,255,255,0.6);
    }
    /* 1) define color de texto por defecto y aplícalo al body */
:root {
  --text: #0f172a; /* color texto en tema claro */
  --muted: #6b7280; /* ya tenías esta */
}
/* tema oscuro: cambia la variable --text */
[data-theme="dark"]{
  --text: #e6eef8;    /* color principal en oscuro (claro) */
  --muted: #94a3b8;   /* puedes ajustar si quieres más contraste */
}
/* aplica el color base a todo el documento para que todo herede correctamente */
body, .card, .container, main, aside {
  color: var(--text);
}
/* 2) asegura que strong y b hereden ese color (y sean claramente visibles) */
strong, b {
  color: inherit;        /* hereda var(--text) del contenedor */
  font-weight: 700;
}
/* 3) si tienes elementos 'muted' que deben seguir grises en ambos temas, mantenlos */
.muted { color: var(--muted); }
/* 4) si quieres que algún pequeño subtítulo no sea tan brillante en dark, ajusta */
[data-theme="dark"] .small { color: var(--muted); }
/* 5) caso extremo: si hay reglas con color fijo (ej: color:#000) podemos sobrescribirlas
   añade esta regla con mayor especificidad para forzar la corrección en oscuro */
[data-theme="dark"] * { color: inherit !important; }
[data-theme="dark"]{ --bg:#0f172a; --card:#0b1220; --muted:#94a3b8; --accent1:#fb7185; --accent2:#f97316; --glass: rgba(255,255,255,0.03); color: #e6eef8 }

  html,body{height:100%;margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI', Roboto,'Helvetica Neue',Arial}
  /* usar todo el ancho disponible; quitar padding del document y evitar scroll global */
  body{background:linear-gradient(180deg,var(--bg),#e6eef8);display:block;padding:0;min-height:100vh;overflow:hidden}
  /* container ocupa el viewport en ancho y alto; el contenido interno se reflowa con grid */
  .container{width:100vw;height:100vh;box-sizing:border-box;padding:12px 18px;display:grid;grid-template-columns:1fr 360px;gap:18px;align-items:start}
  /* hacer que las tarjetas llenen la altura disponible sin provocar scroll del documento */
  main.card{height:100%;overflow:auto}
  aside.card{height:100%;overflow:auto}
  /* time escala responsivamente y evita ser enorme */
  .time{font-size:clamp(28px,6vw,64px)}
  /* ajustes en pantallas pequeñas para garantizar que todo quepa en una sola vista */
  @media (max-height:740px){
    .container{padding:8px 10px;gap:10px}
    main.card, aside.card{padding:10px}
    .time{font-size:clamp(22px,5.5vw,48px)}
  }
    .card{background:var(--card);border-radius:14px;padding:20px;box-shadow:0 6px 22px rgba(16,24,40,0.06)}
    h1{margin:0 0 6px 0;font-size:20px}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    .modes{display:flex;gap:8px;margin-top:14px}
    .mode-btn{padding:8px 12px;border-radius:999px;border:1px solid rgba(15,23,42,0.04);background:transparent;cursor:pointer}
    .mode-btn.active{background:linear-gradient(90deg,var(--accent1),var(--accent2));color:white;border:none}

    .timer{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:22px 12px}
    .time{font-family:ui-monospace,SFMono-Regular,Menlo,monospace;font-size:64px;margin:8px 0}
    .barwrap{width:100%;background:#f1f5f9;border-radius:999px;height:8px;overflow:hidden}
    .bar{height:8px;border-radius:999px;background:linear-gradient(90deg,var(--accent1),var(--accent2));width:0%}

    .controls{display:flex;gap:8px;margin-top:12px}
    button.btn{padding:10px 14px;border-radius:10px;border:none;cursor:pointer}
    button.primary{background:linear-gradient(90deg,var(--accent1),var(--accent2));color:white}
    button.ghost{background:transparent;border:1px solid rgba(15,23,42,0.06)}

    .settings{margin-top:14px;border-top:1px dashed rgba(0,0,0,0.06);padding-top:14px}
    .row{display:flex;gap:10px;align-items:center}
    label.small{font-size:12px;color:var(--muted);width:150px}
    input[type=number],input[type=text],select{padding:8px;border-radius:8px;border:1px solid rgba(15,23,42,0.06);min-width:60px}

    .tasks{display:flex;flex-direction:column;gap:8px}
    .task{display:flex;align-items:center;justify-content:space-between;padding:8px;border-radius:8px;border:1px solid rgba(15,23,42,0.04)}
    .task .left{display:flex;gap:8px;align-items:center}

    .aside-head{display:flex;align-items:center;justify-content:space-between}
    .muted{color:var(--muted);font-size:13px}
    .small{font-size:13px}

    .history{margin-top:12px;max-height:220px;overflow:auto}

    .theme-toggle{cursor:pointer;padding:8px;border-radius:8px;border:1px solid rgba(15,23,42,0.04)}

    footer.note{font-size:12px;color:var(--muted);margin-top:10px}

    @media(max-width:900px){.container{grid-template-columns:1fr;}}
    /* Asegurar que el texto que el usuario escribe sea negro incluso en tema oscuro */
    [data-theme="dark"] input,
    [data-theme="dark"] input[type="text"],
    [data-theme="dark"] input[type="number"],
    [data-theme="dark"] input[type="search"],
    [data-theme="dark"] textarea,
    [data-theme="dark"] select,
    [data-theme="dark"] .task .left div,
    [data-theme="dark"] #newTask,
    [data-theme="dark"] .task span{
      color: #000000 !important;
      caret-color: #000000 !important;
    }
    /* placeholder más oscuro para inputs en tema oscuro */
    [data-theme="dark"] input::placeholder,
    [data-theme="dark"] textarea::placeholder{
      color: rgba(0,0,0,0.5) !important;
    }
  </style>
</head>
<body>
  <!-- SPLASH OVERLAY: poner esto AL INICIO del <body> -->

<div id="splashOverlay" class="splash-overlay" aria-hidden="false" role="dialog" aria-label="Pantalla inicial">
  <div class="splash-inner"> 
    <img id="splashLogo" class="splash-logo" src="logo.jpg.jpeg" alt="Logo Neurofocus">
    <div id="splashTip" class="splash-tip">CONSEJO: BLOQUEA LAS NOTIFICACIONES DE LAS REDES SOCIALES DE TU CELULAR</div>
  </div>
</div>

<style>
/* Splash: pantalla completa, fondo negro y latido */
.splash-overlay{
  position: fixed;
  inset: 0;
  display:flex;
  align-items:center;
  justify-content:center;
  background: #000;
  z-index: 99999;
  opacity: 1;
  transition: opacity 1000ms ease, transform 1000ms ease;
  pointer-events: all;
}

.splash-inner{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 14px;                 /* espacio entre logo y texto */
  text-align: center;        /* centra el texto debajo del logo */
  padding: 12px;
}

/* logo: bloque centrado */
.splash-logo{
  width: 320px;
  max-width: 72%;
  height: auto;
  display: block;
  margin: 0 auto;
  user-select: none;
  -webkit-user-drag: none;
  border-radius: 6px;
  /* la clase 'beating' la añade JS cuando la imagen carga */
}
    /* consejo: texto blanco solo en el overlay inicial, no afecta al resto de la página */
    .splash-overlay .splash-tip{ color: #ffffff !important; font-size:16px; max-width:80%; }
    .splash-tip{ color: #ffffff; font-size:16px; max-width:80%; }

.splash-overlay.hidden{
  opacity: 1;
  transform: scale(2);
  pointer-events: none;
}
.splash-logo{
  width: 820px;
  max-width: 72%;
  height: auto;
  animation: heartbeat 940ms ease-in-out infinite;
  user-select: none;
  -webkit-user-drag: none;
}

@keyframes heartbeat{
  0%   { transform: scale(1); }
  14%  { transform: scale(1.09); }
  28%  { transform: scale(1); }
  42%  { transform: scale(1.07); }
  70%  { transform: scale(1); }
  100% { transform: scale(1); } 
}
.splash-logo.beating {
  animation: heartbeat 940ms ease-in-out infinite;
  filter: drop-shadow(0 12px 24px rgba(0,0,0,0.6));
}
html.splash-active, body.splash-active { overflow: hidden; height: 100%; }
</style>

<script>
(function(){
  const overlay = document.getElementById('splashOverlay');
  const logo = document.getElementById('splashLogo');
  if(!overlay || !logo) return;

  // bloquear scroll mientras dure el splash
  document.documentElement.classList.add('splash-active');
  document.body.classList.add('splash-active');

  // mostrar exactamente 2000 ms y luego ocultar automáticamente
  const VISIBLE_MS = 2000;

  // forzamos que esté visible ahora (por si CSS o algo lo ocultó)
  overlay.style.display = 'flex';
  overlay.style.opacity = '1';

  setTimeout(()=>{
    overlay.classList.add('hidden');
    // eliminar del DOM tras la transición
    setTimeout(()=>{
      if(overlay && overlay.parentNode) overlay.parentNode.removeChild(overlay);
      document.documentElement.classList.remove('splash-active');
      document.body.classList.remove('splash-active');
    }, 420);
  }, VISIBLE_MS);

  // Safety: si algo falla, asegurar que se quite a los 3s
  setTimeout(()=>{
    if(document.body.classList.contains('splash-active')){
      overlay.classList.add('hidden');
      setTimeout(()=>{
        if(overlay && overlay.parentNode) overlay.parentNode.removeChild(overlay);
        document.documentElement.classList.remove('splash-active');
        document.body.classList.remove('splash-active');
      }, 420);
    }
  }, 3000);
})();

</script>
<!-- fin SPLASH -->

  <div class="container" id="app">
    <main class="card">
      <div class="aside-head">
        <div>
          <h1>Organiza tu tiempo</h1>
          <p class="lead">Trabaja en bloques concentrados y toma descansos para aumentar tu productividad.</p>
        </div>
        <div style="display:flex;gap:8px;align-items:center">
          <div class="muted small">Tema</div>
          <div id="themeBtn" class="theme-toggle">Cambiar</div>
        </div>
      </div>

      <div class="modes" style="margin-bottom:6px">
        <button class="mode-btn active" data-mode="work">Trabajo</button>
        <button class="mode-btn" data-mode="short">Descanso corto</button>
        <button class="mode-btn" data-mode="long">Descanso largo</button>
      </div>

      <section class="timer" aria-live="polite">
        <div class="time" id="display">25:00</div>
        <div class="muted small" id="modeLabel">Modo: Trabajo</div>
        <div class="barwrap" aria-hidden="true" style="width:100%;margin-top:14px">
          <div class="bar" id="progress"></div>
        </div>

        <div class="controls">
          <button class="btn primary" id="startPause">Iniciar</button>
          <button class="btn ghost" id="reset">Reiniciar</button>
          <button class="btn ghost" id="skip">Siguiente</button>
        </div>

        <div class="settings">
          <div class="row" style="margin-bottom:8px">
            <label class="small">Trabajo (min)</label>
            <input type="number" id="workMin" min="1" value="25">
            <label class="small" style="margin-left:12px">Desc corto (min)</label>
            <input type="number" id="shortMin" min="1" value="5">
            <label class="small" style="margin-left:12px">Desc largo (min)</label>
            <input type="number" id="longMin" min="1" value="15">
          </div>

          <div class="row" style="margin-top:8px;justify-content:space-between">
            <div style="display:flex;gap:8px;align-items:center">
              <label class="small">Ciclos antes de largo</label>
              <input type="number" id="cyclesBeforeLong" min="1" value="4" style="width:70px">
              <label class="small" style="margin-left:10px">Auto-start</label>
              <input type="checkbox" id="autoStart" checked>
            </div>

            <div style="display:flex;gap:8px;align-items:center">
              <label class="small">Sonido:</label>
              <select id="soundSelect">
                <option value="default">Beep (por defecto)</option>
                <option value="chime">Chime</option>
                <option value="custom">Subir archivo...</option>
              </select>
              <input type="file" id="soundFile" accept="audio/*" style="display:none">
            </div>
          </div>

        </div>

      </section>

      <section style="margin-top:12px">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div class="small muted">Ciclos completados: <strong id="cycles">0</strong></div>
          <div>
            <button class="btn ghost" id="exportData">Exportar datos</button>
            <button class="btn ghost" id="clearData">Resetear</button>
          </div>
        </div>

        <div class="history card" id="historyWrap" style="margin-top:10px;padding:10px;">
          <div class="muted small">Historial de sesiones completadas</div>
          <ul id="historyList" style="margin:8px 0;padding:0;list-style:none"></ul>
        </div>
      </section>

      <footer class="note">Consejo: trabaja en una sola tarea por cada pomodoro. Después de varios ciclos toma un descanso largo.</footer>
    </main>

    <aside class="card">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h3 style="margin:0">Tareas</h3>
        <div class="muted small">Guarda tareas en tu navegador</div>
      </div>

      <div style="display:flex;gap:8px;margin-top:10px">
        <input id="newTask" type="text" placeholder="Nueva tarea..." style="flex:1;padding:8px;border-radius:8px;border:1px solid rgba(15,23,42,0.06)">
        <button class="btn primary" id="addTask">Añadir</button>
      </div>

      <div id="tasks" style="margin-top:10px;max-height:46vh;overflow:auto"></div>

      <div style="margin-top:12px;border-top:1px dashed rgba(0,0,0,0.06);padding-top:10px">
        <div class="small muted">Estadísticas</div>
        <div style="display:flex;gap:8px;margin-top:8px">
          <div class="small">Sesiones totales: <strong id="statSessions">0</strong></div>
          <div class="small">Minutos totales: <strong id="statMinutes">0</strong></div>
        </div>

        <div style="margin-top:12px">
          <small class="muted">Nota: integración con Google Calendar o TODOs requiere autorización y un backend — si quieres puedo preparar una versión con OAuth.</small>
        </div>
      </div>
    </aside>
  </div>


<script>
// ======= App logic ========
const qs = (s, el=document)=>el.querySelector(s);
const qsa = (s, el=document)=>Array.from(el.querySelectorAll(s));

let state = {
  mode: 'work', // work | short | long
  durations: { work: 25*60, short: 5*60, long: 15*60 },
  secondsLeft: 25*60,
  running: false,
  cyclesCompleted: 0,
  cyclesBeforeLong: 4,
  autoStart: true,
  sound: 'default',
  customSoundDataUrl: null,
  stats: { sessions:0, minutes:0 },
  history: [],
};

// Load from localStorage
function loadState(){
  try{
    const raw = localStorage.getItem('pomodoro:data');
    if(raw){
      const parsed = JSON.parse(raw);
      Object.assign(state, parsed);
      // Reiniciar contadores volátiles al recargar la página: ciclos y sesiones no persisten entre reloads
      state.cyclesCompleted = 0;
      if(state.stats) state.stats.sessions = 0;
      // convert minutes to seconds if older format
      if(state.durations.work && state.durations.work < 1000) state.durations.work *= 1; // no-op
    }
  }catch(e){console.warn('load fail',e)}
}
function saveState(){
  const copy = JSON.parse(JSON.stringify(state));
  localStorage.setItem('pomodoro:data', JSON.stringify(copy));
}

loadState();

// Elements
const display = qs('#display');
const modeLabel = qs('#modeLabel');
const progress = qs('#progress');
const startPauseBtn = qs('#startPause');
const resetBtn = qs('#reset');
const skipBtn = qs('#skip');
const cyclesEl = qs('#cycles');
const historyList = qs('#historyList');
const exportBtn = qs('#exportData');
const clearBtn = qs('#clearData');

// ...existing code...
// ===== Theme handling (único bloque, persistente) =====
function applyTheme(t, persist = true){
  if(!t) return;
  document.documentElement.setAttribute('data-theme', t);
  if(persist){
    try{ localStorage.setItem('pomodoro:theme', t); }catch(e){}
  }
}

const savedTheme = localStorage.getItem('pomodoro:theme') || 'light';
// Inicia con el tema guardado (o 'light' si no hay)
applyTheme(savedTheme);

const themeBtn = qs('#themeBtn');
if(themeBtn){
  themeBtn.addEventListener('click', ()=>{
    const next = document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
    applyTheme(next);
  });
}
// ...existing code...

// Settings inputs
const workMin = qs('#workMin');
const shortMin = qs('#shortMin');
const longMin = qs('#longMin');
const cyclesBeforeLongInput = qs('#cyclesBeforeLong');
const autoStartInput = qs('#autoStart');
const soundSelect = qs('#soundSelect');
const soundFile = qs('#soundFile');

// Tasks
const tasksWrap = qs('#tasks');
const newTaskInput = qs('#newTask');
const addTaskBtn = qs('#addTask');
const statSessions = qs('#statSessions');
const statMinutes = qs('#statMinutes');

// Mode buttons
qsa('.mode-btn').forEach(btn=>btn.addEventListener('click',()=>{
  changeMode(btn.dataset.mode);
}));

// Theme handling

// --- Theme handling (NO guardar en localStorage; iniciar siempre en light) ---
function applyTheme(t){
  // aplica el tema únicamente en el DOM, sin persistirlo
  document.documentElement.setAttribute('data-theme', t);
}

// iniciar SIEMPRE en light para que el splash y el tip se vean bien
applyTheme('light');

// cambiar tema durante la sesión (no se guarda)


// Audio: we support default WebAudio beep, and optional uploaded audio
let customAudio = null;
let audioContext = null;
function playDefaultBeep(){
  try{
    audioContext = audioContext || new (window.AudioContext||window.webkitAudioContext)();
    const o = audioContext.createOscillator();
    const g = audioContext.createGain();
    o.type='sine'; o.frequency.value=880;
    o.connect(g); g.connect(audioContext.destination);
    g.gain.setValueAtTime(1,audioContext.currentTime);
    g.gain.exponentialRampToValueAtTime(0.001,audioContext.currentTime+0.4);
    o.start(); o.stop(audioContext.currentTime+0.45);
  }catch(e){console.warn(e)}
}
function playChime(){
  // synthetic short chime
  try{
    audioContext = audioContext || new (window.AudioContext||window.webkitAudioContext)();
    const o = audioContext.createOscillator();
    const o2 = audioContext.createOscillator();
    const g = audioContext.createGain();
    o.type='sine'; o.frequency.value=660;
    o2.type='sine'; o2.frequency.value=990;
    o.connect(g); o2.connect(g); g.connect(audioContext.destination);
    g.gain.setValueAtTime(0.001,audioContext.currentTime);
    g.gain.linearRampToValueAtTime(0.7,audioContext.currentTime+0.02);
    g.gain.exponentialRampToValueAtTime(0.001,audioContext.currentTime+0.7);
    o.start(); o2.start(); o.stop(audioContext.currentTime+0.7); o2.stop(audioContext.currentTime+0.7);
  }catch(e){console.warn(e)}
}
function playSound(){
  if(state.sound === 'custom' && state.customSoundDataUrl){
    if(!customAudio){ customAudio = new Audio(state.customSoundDataUrl); }
    try{ customAudio.currentTime = 0; customAudio.play(); }catch(e){console.warn(e)}
    return;
  }
  if(state.sound === 'chime') return playChime();
  return playDefaultBeep();
}

soundSelect.addEventListener('change', (e)=>{
  const v = e.target.value;
  if(v === 'custom'){
    soundFile.style.display = '';
    soundFile.click();
  } else {
    soundFile.style.display = 'none';
    state.sound = v; saveState();
  }
});

soundFile.addEventListener('change', async (e)=>{
  const f = e.target.files[0];
  if(!f) return;
  const reader = new FileReader();
  reader.onload = ()=>{
    state.sound = 'custom';
    state.customSoundDataUrl = reader.result;
    customAudio = new Audio(state.customSoundDataUrl);
    saveState();
  };
  reader.readAsDataURL(f);
});

// Notification permission
if('Notification' in window && Notification.permission === 'default'){
  Notification.requestPermission().catch(()=>{});
}

// Timer
let interval = null;
function startTimer(){
  if(state.running) return;
  state.running = true; saveState();
  startPauseBtn.textContent = 'Pausar';
  interval = setInterval(()=>{
    state.secondsLeft -= 1;
    if(state.secondsLeft <= 0){
      // Complete
      state.running = false; clearInterval(interval);
      onComplete();
    }
    renderTimer();
  },1000);
}
function pauseTimer(){
  state.running = false; saveState();
  startPauseBtn.textContent = 'Iniciar';
  clearInterval(interval);
}
function resetTimer(){
  state.running = false; clearInterval(interval);
  setModeDurations();
  state.secondsLeft = state.durations[state.mode];
  startPauseBtn.textContent = 'Iniciar';
  saveState(); renderTimer();
}

function skipPhase(){
  // simulate finishing current phase
  state.secondsLeft = 0;
  if(interval) clearInterval(interval);
  onComplete();
}

function onComplete(){
  // play sound + notification
  playSound();
  if('Notification' in window && Notification.permission === 'granted'){
    const title = state.mode === 'work' ? '¡Tiempo de descanso!' : '¡Hora de trabajar!';
    try{ new Notification(title, { body: `Modo: ${state.mode}` }); }catch(e){}
  }
  // record history if was work
  if(state.mode === 'work'){
    state.cyclesCompleted += 1;
    state.stats.sessions += 1;
    state.stats.minutes += Math.round(state.durations.work/60);
    state.history.unshift({ mode: 'work', at: new Date().toISOString(), minutes: Math.round(state.durations.work/60) });
  } else {
    state.history.unshift({ mode: state.mode, at: new Date().toISOString(), minutes: Math.round(state.durations[state.mode]/60) });
  }

  // decide next mode
  if(state.mode === 'work'){
    if(state.cyclesCompleted % state.cyclesBeforeLong === 0){ state.mode = 'long'; }
    else state.mode = 'short';
  } else {
    state.mode = 'work';
  }

  setModeDurations();
  state.secondsLeft = state.durations[state.mode];
  saveState();
  renderAll();

  // auto start next
  if(state.autoStart){
    setTimeout(()=> startTimer(), 700);
  }
}

function setModeDurations(){
  const w = parseInt(workMin.value,10) || 25;
  const s = parseInt(shortMin.value,10) || 5;
  const l = parseInt(longMin.value,10) || 15;
  state.durations.work = w*60; state.durations.short = s*60; state.durations.long = l*60;
  state.cyclesBeforeLong = parseInt(cyclesBeforeLongInput.value,10) || 4;
  state.autoStart = autoStartInput.checked;
}

function changeMode(m){
  state.mode = m;
  setModeDurations();
  state.secondsLeft = state.durations[m];
  state.running = false; clearInterval(interval);
  document.querySelectorAll('.mode-btn').forEach(b=>b.classList.toggle('active', b.dataset.mode===m));
  renderAll(); saveState();
}

function formatTime(sec){
  const mm = Math.floor(sec/60).toString().padStart(2,'0');
  const ss = Math.floor(sec%60).toString().padStart(2,'0');
  return mm+':'+ss;
}

function renderTimer(){
  display.textContent = formatTime(state.secondsLeft);
  modeLabel.textContent = 'Modo: ' + (state.mode === 'work' ? 'Trabajo' : state.mode === 'short' ? 'Descanso corto' : 'Descanso largo');
  const total = state.durations[state.mode] || 1;
  const perc = Math.round((1 - state.secondsLeft/total)*100);
  progress.style.width = perc + '%';
}

function renderHistory(){
  cyclesEl.textContent = state.cyclesCompleted;
  historyList.innerHTML = '';
  state.history.slice(0,80).forEach(h=>{
    const li = document.createElement('li');
    li.style.marginBottom='6px';
    li.style.fontSize='13px';
    li.textContent = `${new Date(h.at).toLocaleString()} — ${h.mode} — ${h.minutes} min`;
    historyList.appendChild(li);
  });
}

function renderTasks(){
  const raw = localStorage.getItem('pomodoro:tasks') || '[]';
  const tasks = JSON.parse(raw);
  tasksWrap.innerHTML = '';
  tasks.forEach(t=>{
    const div = document.createElement('div'); div.className = 'task';
    const left = document.createElement('div'); left.className='left';
    const cb = document.createElement('input'); cb.type='checkbox'; cb.checked = !!t.done;
    cb.addEventListener('change',()=>{ toggleTask(t.id); });
    const span = document.createElement('div'); span.textContent = t.text; span.style.fontSize='14px';
    left.appendChild(cb); left.appendChild(span);
    const right = document.createElement('div');
    const del = document.createElement('button'); del.className='btn ghost'; del.textContent='Eliminar'; del.addEventListener('click',()=>{ removeTask(t.id); });
    right.appendChild(del);
    div.appendChild(left); div.appendChild(right);
    tasksWrap.appendChild(div);
  });
}

function addTask(){
  const text = newTaskInput.value.trim(); if(!text) return;
  const raw = localStorage.getItem('pomodoro:tasks') || '[]';
  const arr = JSON.parse(raw);
  arr.unshift({ id: Date.now(), text, done: false });
  localStorage.setItem('pomodoro:tasks', JSON.stringify(arr));
  newTaskInput.value = '';
  renderTasks();
}
function toggleTask(id){
  const raw = localStorage.getItem('pomodoro:tasks') || '[]';
  const arr = JSON.parse(raw);
  const next = arr.map(x=> x.id===id? {...x, done:!x.done}:x);
  localStorage.setItem('pomodoro:tasks', JSON.stringify(next)); renderTasks();
}
function removeTask(id){
  const raw = localStorage.getItem('pomodoro:tasks') || '[]';
  const arr = JSON.parse(raw).filter(x=>x.id!==id);
  localStorage.setItem('pomodoro:tasks', JSON.stringify(arr)); renderTasks();
}

addTaskBtn.addEventListener('click', addTask);
newTaskInput.addEventListener('keydown',(e)=>{ if(e.key==='Enter') addTask(); });

startPauseBtn.addEventListener('click',()=>{
  if(state.running) pauseTimer(); else startTimer();
});
resetBtn.addEventListener('click',resetTimer);
skipBtn.addEventListener('click',skipPhase);

exportBtn.addEventListener('click',()=>{
  const data = JSON.stringify(state, null, 2);
  const blob = new Blob([data], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href=url; a.download = 'pomodoro-data.json'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
});

clearBtn.addEventListener('click',()=>{
  if(!confirm('¿Borrar todos los datos guardados?')) return;
  localStorage.removeItem('pomodoro:data');
  localStorage.removeItem('pomodoro:tasks');
  state = { mode:'work', durations:{work:25*60,short:5*60,long:15*60}, secondsLeft:25*60, running:false, cyclesCompleted:0, cyclesBeforeLong:4, autoStart:true, sound:'default', customSoundDataUrl:null, stats:{sessions:0,minutes:0}, history:[] };
  saveState(); renderAll(); renderTasks();
});

// load tasks separately
renderTasks();

// initial render
function renderAll(){
  // apply inputs from state
  workMin.value = Math.round(state.durations.work/60);
  shortMin.value = Math.round(state.durations.short/60);
  longMin.value = Math.round(state.durations.long/60);
  cyclesBeforeLongInput.value = state.cyclesBeforeLong;
  autoStartInput.checked = state.autoStart;
  soundSelect.value = state.sound || 'default';
  cyclesEl.textContent = state.cyclesCompleted;
  statSessions.textContent = state.stats.sessions;
  statMinutes.textContent = state.stats.minutes;
  renderTimer(); renderHistory();
}

// initialize durations
setModeDurations();
if(state.mode) changeMode(state.mode);
renderAll();

// keep state updated from inputs
[workMin, shortMin, longMin, cyclesBeforeLongInput].forEach(inp=>inp.addEventListener('change',()=>{
  setModeDurations(); saveState(); renderTimer();
}));
autoStartInput.addEventListener('change',()=>{ state.autoStart = autoStartInput.checked; saveState(); });

// make sure audio context resumed after user gesture
document.addEventListener('click', ()=>{ if(audioContext && audioContext.state==='suspended') audioContext.resume().catch(()=>{}); }, {once:true});

</script>
</body>
</html>

