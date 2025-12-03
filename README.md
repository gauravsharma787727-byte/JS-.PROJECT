<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Digital Clock</title>
<style>
  body {font-family: system-ui, Arial; display:flex;align-items:center;justify-content:center;height:100vh;margin:0;background:#0f172a;color:#e6eef8;}
  .clock {text-align:center;padding:2rem;border-radius:12px;background:linear-gradient(180deg,#111827,#0b1220);box-shadow:0 8px 30px rgba(2,6,23,.6);}
  .time {font-size:4rem;font-weight:700;letter-spacing:2px;}
  .date {margin-top:.5rem;color:#9fb0c8;}
  .controls {margin-top:1rem;}
  button {padding:.5rem 1rem;border-radius:8px;border:0;background:#1f6feb;color:white;cursor:pointer}
  button.secondary {background:#334155}
</style>
</head>
<body>
  <div class="clock" role="application" aria-label="Digital clock">
    <div class="time" id="time">--:--:--</div>
    <div class="date" id="date">Loading date...</div>
    <div class="controls">
      <button id="toggleFormat">Switch to 12-hour</button>
      <button class="secondary" id="showSeconds">Hide Seconds</button>
    </div>
  </div>

<script>
(function(){
  const timeEl = document.getElementById('time');
  const dateEl = document.getElementById('date');
  const toggleBtn = document.getElementById('toggleFormat');
  const showSecondsBtn = document.getElementById('showSeconds');

  let use24 = true;
  let showSeconds = true;

  function pad(n){ return n.toString().padStart(2,'0'); }

  function update(){
    const now = new Date();
    let hrs = now.getHours();
    let suffix = '';
    if(!use24){
      suffix = hrs >= 12 ? ' PM' : ' AM';
      hrs = hrs % 12 || 12;
    }
    const mins = pad(now.getMinutes());
    const secs = pad(now.getSeconds());
    timeEl.textContent = showSeconds ? `${pad(hrs)}:${mins}:${secs}${suffix}` : `${pad(hrs)}:${mins}${suffix}`;
    const options = { weekday:'long', year:'numeric', month:'short', day:'numeric' };
    dateEl.textContent = now.toLocaleDateString(undefined, options);
  }

  toggleBtn.addEventListener('click', () => {
    use24 = !use24;
    toggleBtn.textContent = use24 ? 'Switch to 12-hour' : 'Switch to 24-hour';
    update();
  });

  showSecondsBtn.addEventListener('click', () => {
    showSeconds = !showSeconds;
    showSecondsBtn.textContent = showSeconds ? 'Hide Seconds' : 'Show Seconds';
    update();
  });

  update();
  setInterval(update, 1000);
})();
</script>
</body>
</html>


