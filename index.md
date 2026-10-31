---
layout: default
title: code;music — Процедурный кайф
custom_css: /css/main.css
---

# <span class="gradient-text">code;music</span>
Архив процедурного аудио. Без авторских прав. Чистый JS.

---

### <span class="gradient-text">Внутренний Глитч</span>
*Автор: kpblm4ik*  
Экспериментальный процедурный рок и пост-панк в стиле группы «Кино» и раннего «Дубового Гаайъ».

<div class="track-card">
    <div class="track-header">
        <button class="play-btn" id="rockBtn">PLAY</button>
    </div>
    <div class="code-box">
        <button class="copy-btn" onclick="copyCode('rockCode')">Copy JS</button>
        <pre id="rockCode">// Пост-панк движок на Web Audio API...</pre>
    </div>
</div>

---

### <span class="gradient-text">Монастырская Резня</span>
*Автор: Puppet Combo Fan*  
Тяжёлый, грязный lo-fi хоррор-эмбиент, воссоздающий атмосферу игры Nun Massacre.

<div class="track-card">
    <div class="track-header">
        <button class="play-btn" id="horrorBtn">PLAY</button>
    </div>
    <div class="code-box">
        <button class="copy-btn" onclick="copyCode('horrorCode')">Copy JS</button>
        <pre id="horrorCode">// Хоррор эмбиент (Nun Massacre Style)...</pre>
    </div>
</div>

---

<a href="https://github.com" target="_blank" class="add-track-btn" title="Добавить свой трек">+</a>

{% raw %}
<script id="audio-engine-script">
let audioCtx = null;
let currentPlaying = null;

let rockInterval = null;
let rockStep = 0;
let rockNodes = [];

let horrorNodes = [];
let horrorTimeout = null;

function initAudio() {
    if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
}

const rockBtn = document.getElementById('rockBtn');
const horrorBtn = document.getElementById('horrorBtn');

rockBtn.addEventListener('click', () => {
    initAudio();
    if (currentPlaying === 'rock') {
        stopAll();
    } else {
        stopAll();
        startRock();
        rockBtn.innerText = "STOP";
        rockBtn.classList.add('playing');
        currentPlaying = 'rock';
    }
});

horrorBtn.addEventListener('click', () => {
    initAudio();
    if (currentPlaying === 'horror') {
        stopAll();
    } else {
        stopAll();
        startHorror();
        horrorBtn.innerText = "STOP";
        horrorBtn.classList.add('playing');
        currentPlaying = 'horror';
    }
});

function stopAll() {
    if (rockInterval) clearInterval(rockInterval);
    rockNodes.forEach(n => { try { n.stop(); } catch(e){} });
    rockNodes = [];
    rockStep = 0;
    rockBtn.innerText = "PLAY";
    rockBtn.classList.remove('playing');

    if (horrorTimeout) clearTimeout(horrorTimeout);
    horrorNodes.forEach(n => { try { n.stop(); } catch(e){} });
    horrorNodes = [];
    horrorBtn.innerText = "PLAY";
    horrorBtn.classList.remove('playing');

    currentPlaying = null;
}

function startRock() {
    audioCtx.resume();
    const stepTime = 60 / 120 / 2;
    
    const masterVolume = audioCtx.createGain();
    masterVolume.gain.setValueAtTime(0.5, audioCtx.currentTime);
    masterVolume.connect(audioCtx.destination);

    const delayNode = audioCtx.createDelay();
    delayNode.delayTime.setValueAtTime(0.375, audioCtx.currentTime);
    const delayFeedback = audioCtx.createGain();
    delayFeedback.gain.setValueAtTime(0.3, audioCtx.currentTime);
    delayNode.connect(delayFeedback);
    delayFeedback.connect(delayNode);
    delayNode.connect(masterVolume);

    const bassProg = [,[55.00,55.00,55.00,55.00,55.00,55.00,55.00,55.00],[43.65,43.65,43.65,43.65,43.65,43.65,43.65,43.65],[65.41,65.41,65.41,65.41,65.41,65.41,65.41,65.41],[49.00,49.00,49.00,49.00,49.00,49.00,49.00,49.00]];
    const guitarProg = [[220,261.63,329.63,440,329.63,261.63,329.63,440],[174.61,220,261.63,349.23,261.63,220,261.63,349.23],[261.63,329.63,392,523.25,392,329.63,392,523.25],[196,246.94,293.66,392,293.66,246.94,293.66,392]];

    function playStep() {
        const time = audioCtx.currentTime + 0.02;
        const chord = Math.floor((rockStep / 8) % 4);
        const s = rockStep % 8;

        if (s === 0 || s === 4) {
            const k = audioCtx.createOscillator(); const kg = audioCtx.createGain();
            k.connect(kg); kg.connect(masterVolume); k.frequency.setValueAtTime(130, time);
            k.frequency.exponentialRampToValueAtTime(0.01, time + 0.12); kg.gain.setValueAtTime(1, time);
            kg.gain.exponentialRampToValueAtTime(0.01, time + 0.12); k.start(time); k.stop(time + 0.13);
        }
        if (s === 2 || s === 6) {
            const sn = audioCtx.createOscillator(); const sg = audioCtx.createGain();
            sn.type = 'triangle'; sn.connect(sg); sg.connect(masterVolume); sn.frequency.setValueAtTime(180, time);
            sg.gain.setValueAtTime(0.5, time); sg.gain.exponentialRampToValueAtTime(0.01, time + 0.08);
            sn.start(time); sn.stop(time + 0.09);
        }

        if (s !== 3 && s !== 7) {
            const b = audioCtx.createOscillator(); const bg = audioCtx.createGain(); const bf = audioCtx.createBiquadFilter();
            b.type = 'sawtooth'; b.frequency.setValueAtTime(bassProg[chord][s], time); bf.type = 'lowpass'; bf.frequency.setValueAtTime(350, time);
            bg.gain.setValueAtTime(0.3, time); bg.gain.exponentialRampToValueAtTime(0.01, time + stepTime);
            b.connect(bf); bf.connect(bg); bg.connect(masterVolume); b.start(time); b.stop(time + stepTime);
        }

        const g1 = audioCtx.createOscillator(); const g2 = audioCtx.createOscillator(); const gg = audioCtx.createGain();
        g1.type = 'triangle'; g1.frequency.setValueAtTime(guitarProg[chord][s], time);
        g2.type = 'sawtooth'; g2.frequency.setValueAtTime(guitarProg[chord][s] + 1.2, time);
        gg.gain.setValueAtTime(0.1, time); gg.gain.exponentialRampToValueAtTime(0.001, time + 0.5);
        g1.connect(gg); g2.connect(gg); gg.connect(masterVolume); gg.connect(delayNode);
        g1.start(time); g2.start(time); g1.stop(time + 0.5); g2.stop(time + 0.5);

        rockStep = (rockStep + 1) % 32;
    }
    rockInterval = setInterval(playStep, stepTime * 1000);
}

function startHorror() {
    audioCtx.resume();
    const comp = audioCtx.createDynamicsCompressor();
    comp.connect(audioCtx.destination);

    const dist = audioCtx.createWaveShaper();
    const curve = new Float32Array(44100);
    for (let i = 0; i < 44100; ++i) { const x = (i * 2) / 44100 - 1; curve[i] = (53 * x) / (Math.PI + 50 * Math.abs(x)); }
    dist.curve = curve; dist.connect(comp);

    const o1 = audioCtx.createOscillator(); const o2 = audioCtx.createOscillator(); const dg = audioCtx.createGain();
    o1.type = 'sawtooth'; o1.frequency.setValueAtTime(32, audioCtx.currentTime);
    o2.type = 'square'; o2.frequency.setValueAtTime(32.5, audioCtx.currentTime);
    dg.gain.setValueAtTime(0.3, audioCtx.currentTime);
    o1.connect(dg); o2.connect(dg); dg.connect(dist);
    o1.start(); o2.start();
    horrorNodes.push(o1, o2);

    function triggerScreech() {
        const sOsc = audioCtx.createOscillator(); const sGain = audioCtx.createGain();
        sOsc.type = 'sawtooth'; const f = 800 + Math.random() * 400;
        sOsc.frequency.setValueAtTime(f, audioCtx.currentTime);
        sOsc.frequency.exponentialRampToValueAtTime(f * 0.3, audioCtx.currentTime + 2);
        sGain.gain.setValueAtTime(0.001, audioCtx.currentTime);
        sGain.gain.linearRampToValueAtTime(0.03, audioCtx.currentTime + 0.2);
        sGain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 2);
        sOsc.connect(sGain); sGain.connect(comp);
        sOsc.start(); sOsc.stop(audioCtx.currentTime + 2.1);
        horrorTimeout = setTimeout(triggerScreech, 4000 + Math.random() * 4000);
    }
    triggerScreech();
}

document.getElementById('rockCode').innerText = startRock.toString();
document.getElementById('horrorCode').innerText = startHorror.toString();

function copyCode(id) {
    navigator.clipboard.writeText(document.getElementById(id).innerText);
    alert('Код трека скопирован!');
}
</script>
{% endraw %}
