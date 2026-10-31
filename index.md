---
layout: null
title: code;music — Процедурный кайф
---

<link rel="stylesheet" href="/codemusic/css/main.css">

<div class="wrapper">

  <div class="gradient-text">code;music</div>
  <div class="catalog-subtitle">Архив процедурного аудио. Без авторских прав. Чистый JS.</div>

  <!-- ТРЕК 1 -->
  <div class="track-card">
    <div class="track-header">
      <div class="track-title">Внутренний Глитч</div>
      <button class="play-btn" id="rockBtn">PLAY</button>
    </div>
    
    <div class="track-controls">
      <div class="control-item">
        <label>Темп (BPM):</label>
        <input type="range" min="60" max="200" value="120">
      </div>
      <div class="control-item">
        <label>Эхо (Delay):</label>
        <input type="range" min="0" max="100" value="35">
      </div>
    </div>

    <div class="code-wrapper">
      <button class="copy-action-btn" onclick="copyCode('rockCode')">Copy JS</button>
      <pre id="rockCode">// Код движка загружается...</pre>
    </div>
  </div>

  <!-- ТРЕК 2 -->
  <div class="track-card">
    <div class="track-header">
      <div class="track-title">Монастырская Резня</div>
      <button class="play-btn" id="horrorBtn">PLAY</button>
    </div>

    <div class="track-controls">
      <div class="control-item">
        <label>Темп (BPM):</label>
        <input type="range" min="60" max="200" value="100">
      </div>
      <div class="control-item">
        <label>Искажение:</label>
        <input type="range" min="0" max="100" value="70">
      </div>
    </div>

    <div class="code-wrapper">
      <button class="copy-action-btn" onclick="copyCode('horrorCode')">Copy JS</button>
      <pre id="horrorCode">// Код движка загружается...</pre>
    </div>
  </div>

  <div class="footer">
    © 2026 codemusic – сделано мастером-конструктором
  </div>

</div>

{% raw %}
<script id="audio-engine-script">
// Твой JS-скрипт без изменений (вставь его сюда полностью, от let audioCtx до конца функции copyCode)
</script>
{% endraw %}
