---
layout: default
title: code;music — Процедурный кайф
---

<div class="wrapper">
  <h1 class="gradient-text">code;music</h1>
  <p class="catalog-subtitle">Архив процедурного аудио. Без авторских прав. Чистый JS.</p>

  <div id="tracks">
    <p class="catalog-subtitle">Треков пока нет. Нажми на плюс, чтобы добавить свой!</p>
  </div>

  <div class="footer">© 2026 codemusic – сделано мастером-конструктором</div>
</div>

<button class="floating-add-btn" id="openModalBtn" aria-label="Добавить трек">+</button>

<div class="modal-overlay" id="modalOverlay">
  <div class="modal-card">
    <div class="modal-header">
      <h2>Добавить трек</h2>
      <button class="close-btn" id="closeModalBtn" aria-label="Закрыть">×</button>
    </div>

    <div class="modal-body">
      <div class="input-item">
        <label for="trackAuthor">Автор трека:</label>
        <input type="text" id="trackAuthor" placeholder="Твой никнейм">
      </div>

      <div class="input-item">
        <label for="trackCode">Код трека (JS):</label>
        <textarea id="trackCode" placeholder="// Вставь свой JS код движка сюда..."></textarea>
      </div>

      <div class="checkbox-item">
        <input type="checkbox" id="licenseAgreement">
        <label for="licenseAgreement">Я соглашаюсь с условиями платформы и лицензией CC0</label>
      </div>

      <button class="submit-btn" id="submitTrackBtn" disabled>Опубликовать</button>
    </div>
  </div>
</div>

<script>
  const openModalBtn = document.getElementById('openModalBtn');
  const closeModalBtn = document.getElementById('closeModalBtn');
  const modalOverlay = document.getElementById('modalOverlay');
  const licenseAgreement = document.getElementById('licenseAgreement');
  const submitTrackBtn = document.getElementById('submitTrackBtn');
  const trackAuthor = document.getElementById('trackAuthor');
  const trackCode = document.getElementById('trackCode');

  const REPO_NEW_FILE = 'https://github.com/kpblm4ik/codemusic/new/main';
  const MAX_URL_LENGTH = 7000; // GitHub не принимает слишком длинные ссылки

  openModalBtn.addEventListener('click', () => modalOverlay.classList.add('active'));
  closeModalBtn.addEventListener('click', () => modalOverlay.classList.remove('active'));
  modalOverlay.addEventListener('click', (e) => {
    if (e.target === modalOverlay) modalOverlay.classList.remove('active');
  });

  licenseAgreement.addEventListener('change', () => {
    submitTrackBtn.disabled = !licenseAgreement.checked;
  });

  submitTrackBtn.addEventListener('click', async () => {
    const rawCode = trackCode.value.trim();
    if (!rawCode) {
      alert('Пожалуйста, вставь код трека!');
      return;
    }

    // Безопасное имя файла: только латиница, цифры, - и _; плюс время, чтобы не совпадало
    const cleanAuthor = trackAuthor.value.trim().replace(/[^a-zA-Z0-9-_]/g, '') || 'track';
    const fileName = cleanAuthor + '-' + Date.now() + '.js';

    const params = 'filename=' + encodeURIComponent('tracks/' + fileName);
    const fullUrl = REPO_NEW_FILE + '?' + params + '&value=' + encodeURIComponent(rawCode);

    if (fullUrl.length <= MAX_URL_LENGTH) {
      window.open(fullUrl, '_blank');
    } else {
      // Код слишком длинный для ссылки: копируем его и открываем пустую форму GitHub
      try {
        await navigator.clipboard.writeText(rawCode);
        alert('Код длинный, поэтому он скопирован в буфер. Вставь его на странице GitHub.');
      } catch (err) {
        alert('Код слишком длинный для ссылки. Скопируй его вручную и вставь на странице GitHub.');
      }
      window.open(REPO_NEW_FILE + '?' + params, '_blank');
    }
  });
</script>
