---
layout: null
title: code;music — Процедурный кайф
---

<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/codemusic/css/main.css">

<div class="wrapper">

  <div class="gradient-text">code;music</div>
  <div class="catalog-subtitle">Архив процедурного аудио. Без авторских прав. Чистый JS.</div>

  <!-- Сюда в будущем будут добавляться новые треки из Pull Requests -->
  <div id="tracks-container">
    <div style="color: #666; font-size: 0.9rem; margin-top: 50px;">Треков пока нет. Нажми на плюс, чтобы добавить свой!</div>
  </div>

  <div class="footer">
    © 2026 codemusic – сделано мастером-конструктором
  </div>

</div>

<!-- ФОНОВАЯ КНОПКА ПЛЮСА -->
<button class="floating-add-btn" id="openModalBtn">+</button>

<!-- МОДАЛЬНОЕ ОКНО -->
<div class="modal-overlay" id="modalOverlay">
  <div class="modal-card">
    <div class="modal-header">
      <div class="modal-title">Добавить трек</div>
      <button class="modal-close-btn" id="closeModalBtn">×</button>
    </div>
    
    <div class="modal-body">
      <div class="input-item">
        <label>Автор трека:</label>
        <input type="text" id="trackAuthor" placeholder="Твой никнейм">
      </div>
      
      <div class="input-item">
        <label>Код трека (JS):</label>
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
  // Логика работы модального окна
  const openModalBtn = document.getElementById('openModalBtn');
  const closeModalBtn = document.getElementById('closeModalBtn');
  const modalOverlay = document.getElementById('modalOverlay');
  const licenseAgreement = document.getElementById('licenseAgreement');
  const submitTrackBtn = document.getElementById('submitTrackBtn');
  
  const trackAuthor = document.getElementById('trackAuthor');
  const trackCode = document.getElementById('trackCode');

  // Открыть и закрыть
  openModalBtn.addEventListener('click', () => {
    modalOverlay.classList.add('active');
  });

  closeModalBtn.addEventListener('click', () => {
    modalOverlay.classList.remove('active');
  });

  // Закрытие по клику на фон
  modalOverlay.addEventListener('click', (e) => {
    if (e.target === modalOverlay) modalOverlay.classList.remove('active');
  });

  // Активация кнопки Опубликовать при нажатии на галочку CC0
  licenseAgreement.addEventListener('change', () => {
    if (licenseAgreement.checked) {
      submitTrackBtn.removeAttribute('disabled');
    } else {
      submitTrackBtn.setAttribute('disabled', 'true');
    }
  });

  // Перенаправление на GitHub для создания файла и Pull Request
  submitTrackBtn.addEventListener('click', () => {
    const rawAuthor = trackAuthor.value.trim() || 'Anonymous';
    const rawCode = trackCode.value.trim();
    
    if (!rawCode) {
      alert('Пожалуйста, вставь код трека!');
      return;
    }

    // Делаем имя файла безопасным для URL
    const safeAuthor = encodeURIComponent(rawAuthor.replace(/[^a-zA-Z0-9-_]/g, ''));
    const code = encodeURIComponent(rawCode);

    // Прямая безопасная ссылка на создание нового js-файла в папке tracks твоего репозитория.
    // GitHub сам предложит пользователю сделать форк и создать Pull Request.
    const githubUrl = 'https://github.com' + safeAuthor + '.js&value=' + code;
    
    window.open(githubUrl, '_blank');
  });
</script>
