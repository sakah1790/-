<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="theme-color" content="#ff8fa3">
    <title>Для моей любимой 💖</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,300;0,500;0,700;1,300&display=swap" rel="stylesheet">

<style>
:root {
    --bg1: #fff0f3;
    --bg2: #ffcbd5;
    --env: #ff8fa3;
    --env2: #ff718c;
    --env3: #e85d7a;
    --paper: #ffffff;
    --heart: #ff4165;
    --text: #4a4a4a;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    -webkit-tap-highlight-color: transparent;
}

html, body {
    width: 100%;
    height: 100%;
    overflow: hidden;
}

body {
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 16px;
    background:
        radial-gradient(circle at 20% 20%, rgba(255,255,255,.75), transparent 30%),
        radial-gradient(circle at 80% 80%, rgba(255,143,163,.35), transparent 40%),
        linear-gradient(135deg, var(--bg1), var(--bg2));
    font-family: 'Montserrat', sans-serif;
}

/* --- ФОН С СЕРДЕЧКАМИ --- */
.hearts-bg {
    position: fixed;
    inset: 0;
    z-index: 0;
    overflow: hidden;
    pointer-events: none;
}

.falling-heart {
    position: absolute;
    top: -50px;
    color: rgba(255, 65, 101, 0.22);
    font-size: 20px;
    line-height: 1;
    user-select: none;
    will-change: transform, opacity;
    animation: fall linear infinite;
}

@keyframes fall {
    0%   { transform: translate3d(0, -40px, 0) rotate(0deg); opacity: 0; }
    10%  { opacity: 1; }
    90%  { opacity: 1; }
    100% { transform: translate3d(var(--drift, 0px), 110vh, 0) rotate(360deg); opacity: 0; }
}

/* --- СЦЕНА С КОНВЕРТОМ --- */
.envelope-scene {
    position: relative;
    z-index: 2;
    width: min(320px, 85vw);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 28px;
}

.envelope-float {
    width: 100%;
    animation: floatEnvelope 3.8s ease-in-out infinite;
}

.envelope-scene.open .envelope-float {
    animation: none;
}

@keyframes floatEnvelope {
    0%, 100% { transform: translateY(0) rotateZ(0deg); }
    50%      { transform: translateY(-8px) rotateZ(-0.5deg); }
}

/* --- КОНВЕРТ --- */
.envelope {
    position: relative;
    width: 100%;
    aspect-ratio: 320 / 220;
    background: linear-gradient(180deg, var(--env) 0%, var(--env2) 100%);
    border-radius: 0 0 14px 14px;
    box-shadow:
        0 22px 55px rgba(191, 62, 91, 0.28),
        0 6px 14px rgba(191, 62, 91, 0.15),
        inset 0 -2px 0 rgba(0,0,0,0.05);
    transition: transform 0.18s ease, box-shadow 0.25s ease;
}

/* Прозрачная кнопка-накладка поверх конверта.
   Именно она ловит клик — это нативный <button>, работает везде. */
.envelope-btn {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    border: none;
    background: transparent;
    cursor: pointer;
    z-index: 20;
    border-radius: 0 0 14px 14px;
    -webkit-appearance: none;
    appearance: none;
    font-size: 0;
    color: transparent;
    padding: 0;
}

.envelope-btn:active {
    background: rgba(0,0,0,0.04);
}

.envelope-btn:focus-visible {
    outline: 3px solid rgba(255, 65, 101, 0.6);
    outline-offset: 4px;
}

.envelope::before {
    content: "";
    position: absolute;
    inset: 0;
    background:
        linear-gradient(to bottom left,  var(--env2) 0%, var(--env2) 50%, transparent 50%),
        linear-gradient(to bottom right, var(--env2) 0%, var(--env2) 50%, transparent 50%);
    border-radius: 0 0 14px 14px;
    z-index: 3;
    pointer-events: none;
}

/* --- ВЕРХНИЙ КЛАПАН --- */
.flap {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 50%;
    background: linear-gradient(180deg, var(--env3) 0%, var(--env2) 100%);
    clip-path: polygon(0 0, 100% 0, 50% 100%);
    transform-origin: top center;
    transform: rotateX(0deg);
    transition:
        transform 0.7s cubic-bezier(0.65, 0, 0.35, 1),
        background 0.4s ease;
    z-index: 6;
    pointer-events: none;
    border-radius: 14px 14px 0 0;
    backface-visibility: hidden;
}

.envelope-scene.open .flap {
    transform: rotateX(180deg);
    background: linear-gradient(0deg, var(--env) 0%, var(--env2) 100%);
    z-index: 1;
}

/* --- СЕРДЕЧКО --- */
.heart {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 34px;
    height: 34px;
    margin: -17px 0 0 -17px;
    background: var(--heart);
    transform: rotate(-45deg) scale(1);
    z-index: 8;
    transition:
        transform 0.45s cubic-bezier(0.5, 1.5, 0.5, 1),
        opacity 0.35s ease;
    box-shadow: 0 5px 16px rgba(255, 65, 101, 0.5);
    pointer-events: none;
    border-radius: 4px;
}

.heart::before,
.heart::after {
    content: "";
    position: absolute;
    width: 34px;
    height: 34px;
    background: var(--heart);
    border-radius: 50%;
}

.heart::before { top: -17px; left: 0; }
.heart::after  { left: 17px;  top: 0; }

.envelope-scene:not(.open) .heart {
    animation: heartPulse 1.6s ease-in-out infinite;
}

.envelope-scene.open .heart {
    transform: rotate(-45deg) scale(0) translateY(-10px);
    opacity: 0;
    animation: none;
}

@keyframes heartPulse {
    0%, 100% {
        box-shadow: 0 5px 16px rgba(255, 65, 101, 0.45);
        transform: rotate(-45deg) scale(1);
    }
    50% {
        box-shadow: 0 5px 28px rgba(255, 65, 101, 0.9);
        transform: rotate(-45deg) scale(1.08);
    }
}

/* --- ПОДСКАЗКА --- */
.hint {
    color: var(--heart);
    font-size: 15px;
    font-weight: 500;
    text-align: center;
    animation: hintPulse 1.6s ease-in-out infinite;
    transition: opacity 0.3s ease, transform 0.3s ease;
    pointer-events: none;
}

.envelope-scene.open .hint {
    opacity: 0;
    transform: translateY(10px);
}

@keyframes hintPulse {
    0%, 100% { opacity: 0.65; transform: translateY(0); }
    50%      { opacity: 1;    transform: translateY(-3px); }
}

/* ============================================================
   ПИСЬМО — НА ВЕСЬ ЭКРАН
   ============================================================ */
.letter-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999;
    display: none;               /* по умолчанию скрыто */
    align-items: stretch;
    justify-content: center;
    padding:
        calc(env(safe-area-inset-top) + 16px)
        calc(env(safe-area-inset-right) + 16px)
        calc(env(safe-area-inset-bottom) + 16px)
        calc(env(safe-area-inset-left) + 16px);
    background: linear-gradient(160deg, var(--bg1) 0%, var(--bg2) 100%);
    opacity: 0;
    transition: opacity 0.4s ease;
}

.letter-overlay.open {
    display: flex;               /* показываем */
    opacity: 1;
}

.letter-card {
    flex: 1;
    max-width: 540px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    background: var(--paper);
    border-radius: 24px;
    box-shadow:
        0 26px 70px rgba(191, 62, 91, 0.38),
        0 10px 24px rgba(191, 62, 91, 0.18);
    padding: 28px 22px 20px;
    position: relative;
    overflow: hidden;
    animation: cardIn 0.5s cubic-bezier(0.2, 0.9, 0.3, 1.1) both;
}

@keyframes cardIn {
    from { transform: scale(0.92); opacity: 0; }
    to   { transform: scale(1);    opacity: 1; }
}

.letter-card::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 6px;
    background: linear-gradient(90deg, var(--heart), var(--env), var(--heart));
    background-size: 200% 100%;
    animation: shimmer 3s linear infinite;
}

@keyframes shimmer {
    0%   { background-position: 0% 50%; }
    100% { background-position: 200% 50%; }
}

.letter-scroll {
    flex: 1;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
    padding: 6px 6px 10px;
    scrollbar-width: thin;
    scrollbar-color: var(--heart) transparent;
}

.letter-scroll::-webkit-scrollbar { width: 4px; }
.letter-scroll::-webkit-scrollbar-track { background: transparent; }
.letter-scroll::-webkit-scrollbar-thumb {
    background: var(--heart);
    border-radius: 4px;
}

.letter-content {
    text-align: center;
    color: var(--text);
    font-size: 15px;
    line-height: 1.7;
    font-weight: 300;
}

.letter-content h1 {
    font-size: 21px;
    line-height: 1.3;
    color: var(--heart);
    font-weight: 700;
    margin-bottom: 18px;
}

.letter-content p {
    margin-bottom: 13px;
}

.letter-content p:last-of-type {
    margin-bottom: 0;
}

.signature {
    margin-top: 22px !important;
    font-style: italic;
    font-weight: 500 !important;
    color: var(--heart);
    font-size: 15px;
}

.letter-overlay.open .letter-content > * {
    animation: fadeInUp 0.5s ease both;
}

.letter-overlay.open .letter-content h1  { animation-delay: 0.25s; }
.letter-overlay.open .letter-content p:nth-of-type(1) { animation-delay: 0.35s; }
.letter-overlay.open .letter-content p:nth-of-type(2) { animation-delay: 0.45s; }
.letter-overlay.open .letter-content p:nth-of-type(3) { animation-delay: 0.55s; }
.letter-overlay.open .letter-content p:nth-of-type(4) { animation-delay: 0.65s; }
.letter-overlay.open .letter-content p:nth-of-type(5) { animation-delay: 0.75s; }
.letter-overlay.open .signature { animation-delay: 0.85s; }

@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(14px); }
    to   { opacity: 1; transform: translateY(0); }
}

/* --- КНОПКА ЗАКРЫТИЯ --- */
.close-btn {
    margin-top: 16px;
    flex-shrink: 0;
    width: 100%;
    padding: 16px 20px;
    border: none;
    border-radius: 50px;
    background: linear-gradient(135deg, var(--env), var(--heart));
    color: #fff;
    font-family: inherit;
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 0.3px;
    cursor: pointer;
    box-shadow:
        0 12px 26px rgba(255, 65, 101, 0.4),
        0 4px 10px rgba(255, 65, 101, 0.25);
    transition: transform 0.15s ease, box-shadow 0.2s ease;
    -webkit-appearance: none;
    appearance: none;
}

.close-btn:active {
    transform: scale(0.96);
    box-shadow:
        0 6px 14px rgba(255, 65, 101, 0.5),
        0 2px 6px rgba(255, 65, 101, 0.3);
}

/* --- АДАПТИВ --- */
@media (max-height: 620px) {
    .letter-card { padding: 22px 18px 16px; }
    .letter-content { font-size: 14px; line-height: 1.6; }
    .letter-content h1 { font-size: 18px; margin-bottom: 14px; }
    .close-btn { padding: 13px 18px; font-size: 15px; }
    .envelope-scene { gap: 20px; }
}

@media (max-width: 360px) {
    .letter-content { font-size: 13.5px; }
    .letter-content h1 { font-size: 17px; }
    .letter-card { padding: 20px 16px 14px; }
}

@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
    .falling-heart { display: none; }
}
</style>

</head>
<body>

    <div class="hearts-bg" id="heartsBg" aria-hidden="true"></div>

    <!-- Сцена с конвертом -->
    <div class="envelope-scene" id="envelopeScene">
        <div class="envelope-float">
            <div class="envelope">
                <div class="flap"></div>
                <div class="heart"></div>
                <!-- Нативная кнопка ловит клик — работает везде -->
                <button class="envelope-btn" id="envelopeBtn" type="button" aria-label="Открыть письмо"></button>
            </div>
        </div>
        <div class="hint" id="hint">Нажми на конверт 💌</div>
    </div>

    <!-- Письмо на весь экран -->
    <div class="letter-overlay" id="letterOverlay">
        <div class="letter-card">
            <div class="letter-scroll">
                <div class="letter-content">
                    <h1>Привет, любимая! ❤️</h1>
                    <p>Решил написать тебе, потому что в коротких сообщениях сложно передать всё, что чувствую.</p>
                    <p>Знаешь, я часто думаю о том, как мне с тобой повезло. С твоим появлением в моей жизни стало больше тепла, света и радости.</p>
                    <p>Мне очень нравится проводить с тобой время: говорить обо всём и ни о чём, смеяться до слёз или просто молчать рядом — и в этом молчании тоже есть что-то особенное.</p>
                    <p>С тобой мне легко и спокойно. Ты удивительная — с твоим характером, улыбкой и той самой энергетикой, которая делает каждый день ярче.</p>
                    <p>Спасибо тебе за поддержку, нежность и за то, что ты просто есть. Я тебя очень люблю и очень ценю.</p>
                    <p class="signature">Твой навеки ✨</p>
                </div>
            </div>
            <button class="close-btn" id="closeBtn" type="button">Закрыть 💖</button>
        </div>
    </div>

<script>
(function () {
    'use strict';

    var scene    = document.getElementById('envelopeScene');
    var btn      = document.getElementById('envelopeBtn');
    var overlay  = document.getElementById('letterOverlay');
    var closeBtn = document.getElementById('closeBtn');
    var heartsBg = document.getElementById('heartsBg');

    function openLetter() {
        scene.classList.add('open');
        overlay.classList.add('open');
    }

    function closeLetter() {
        scene.classList.remove('open');
        overlay.classList.remove('open');
    }

    // Просто и надёжно: onclick на нативной кнопке
    btn.addEventListener('click', openLetter);
    closeBtn.addEventListener('click', closeLetter);

    // ESC на десктопе
    document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape') closeLetter();
    });

    // --- Фон с сердечками ---
    var symbols = ['❤️', '💖', '💕', '🌸', '✨', '💗'];
    var count = window.matchMedia('(max-width: 600px)').matches ? 12 : 20;
    var fragment = document.createDocumentFragment();

    for (var i = 0; i < count; i++) {
        var heart = document.createElement('span');
        heart.className = 'falling-heart';
        heart.textContent = symbols[Math.floor(Math.random() * symbols.length)];
        heart.style.left = (Math.random() * 100).toFixed(2) + 'vw';
        heart.style.setProperty('--drift', Math.round(Math.random() * 120 - 60) + 'px');
        heart.style.animationDuration = (Math.random() * 4 + 5).toFixed(2) + 's';
        heart.style.animationDelay = (Math.random() * 6).toFixed(2) + 's';
        heart.style.fontSize = (Math.random() * 15 + 14).toFixed(1) + 'px';
        fragment.appendChild(heart);
    }

    heartsBg.appendChild(fragment);
})();
</script>
</body>
</html>
