<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Для моей любимой 💖</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,300;0,500;0,700;1,300&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg-color: #fff0f3;
            --envelope-color: #ff8fa3;
            --envelope-dark: #ff758f;
            --letter-color: #ffffff;
            --heart-color: #ff4d6d;
            --text-color: #4a4a4a;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        html, body {
            height: 100%;
        }

        body {
            min-height: 100vh;
            min-height: 100dvh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #fff0f3 0%, #ffccd5 100%);
            font-family: 'Montserrat', sans-serif;
            overflow: hidden;
            position: relative;
            padding: 20px;
            -webkit-tap-highlight-color: transparent;
        }

        /* --- ФОН С ПАДАЮЩИМИ СЕРДЕЧКАМИ --- */
        .hearts-bg {
            position: fixed;
            inset: 0;
            z-index: 1;
            pointer-events: none;
            overflow: hidden;
        }

        .falling-heart {
            position: absolute;
            top: -40px;
            color: rgba(255, 77, 109, 0.18);
            font-size: 20px;
            animation: fall linear infinite;
            will-change: transform, opacity;
            user-select: none;
        }

        @keyframes fall {
            0% {
                transform: translate3d(0, -20px, 0) rotate(0deg);
                opacity: 0;
            }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% {
                transform: translate3d(0, 105vh, 0) rotate(360deg);
                opacity: 0;
            }
        }

        /* --- КОНВЕРТ --- */
        .wrapper {
            position: relative;
            cursor: pointer;
            z-index: 10;
            margin-top: 50px;
            outline: none;
            transition: transform 0.3s ease;
            animation: floatEnvelope 4s ease-in-out infinite;
        }

        .wrapper:hover {
            transform: scale(1.02);
        }

        .wrapper:focus-visible {
            filter: drop-shadow(0 0 12px rgba(255, 77, 109, 0.6));
        }

        .wrapper.open {
            animation: none;
            transform: none;
        }

        @keyframes floatEnvelope {
            0%, 100% { transform: translateY(0); }
            50%      { transform: translateY(-6px); }
        }

        .envelope {
            position: relative;
            width: 320px;
            height: 220px;
            background-color: var(--envelope-color);
            box-shadow: 0 15px 35px rgba(255, 117, 143, 0.35);
            border-bottom-left-radius: 12px;
            border-bottom-right-radius: 12px;
        }

        .envelope::before {
            content: '';
            position: absolute;
            inset: 0;
            border-style: solid;
            border-width: 110px 160px 110px 160px;
            border-color: transparent var(--envelope-dark) var(--envelope-dark) var(--envelope-dark);
            border-bottom-left-radius: 12px;
            border-bottom-right-radius: 12px;
            z-index: 3;
            pointer-events: none;
        }

        .flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 0;
            border-style: solid;
            border-width: 115px 160px 0 160px;
            border-color: var(--envelope-dark) transparent transparent transparent;
            transform-origin: top;
            transition: transform 0.4s ease-in-out 0.2s,
                        border-color 0.3s ease 0.2s,
                        z-index 0s linear 0.4s;
            z-index: 4;
            backface-visibility: hidden;
        }

        /* --- СЕРДЕЧКО-ЗАМОЧЕК --- */
        .heart {
            position: absolute;
            top: 100px;
            left: 145px;
            width: 30px;
            height: 30px;
            background-color: var(--heart-color);
            transform: rotate(-45deg) scale(1);
            z-index: 5;
            transition: transform 0.35s ease-in-out 0.2s, opacity 0.3s ease 0.2s;
            box-shadow: 0 4px 14px rgba(255, 77, 109, 0.5);
        }

        /* Пульс — на дочернем псевдо-элементе, чтобы не конфликтовать с transform родителя */
        .heart::before,
        .heart::after {
            content: '';
            position: absolute;
            width: 30px;
            height: 30px;
            background-color: var(--heart-color);
            border-radius: 50%;
        }

        .heart::before { top: -15px; left: 0; }
        .heart::after  { left: 15px; top: 0; }

        .wrapper:not(.open) .heart {
            animation: heartPulse 1.8s ease-in-out infinite;
        }

        @keyframes heartPulse {
            0%, 100% { box-shadow: 0 4px 14px rgba(255, 77, 109, 0.5); }
            50%      { box-shadow: 0 4px 22px rgba(255, 77, 109, 0.9); }
        }

        /* --- ПИСЬМО --- */
        .letter {
            position: absolute;
            bottom: 10px;
            left: 15px;
            width: 290px;
            height: 190px;
            background-color: var(--letter-color);
            border-radius: 8px;
            padding: 22px 18px;
            box-shadow: 0 0 15px rgba(0,0,0,0.05);
            transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1) 0.1s,
                        height   0.6s cubic-bezier(0.4, 0, 0.2, 1) 0.1s;
            z-index: 2;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .letter-text {
            font-size: 13.5px;
            line-height: 1.6;
            color: var(--text-color);
            text-align: center;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.5s ease 0.55s, transform 0.5s ease 0.55s;
            max-height: 100%;
            overflow-y: auto;
            padding-right: 6px;
            scrollbar-width: thin;
            scrollbar-color: var(--heart-color) transparent;
        }

        .letter-text::-webkit-scrollbar {
            width: 5px;
        }
        .letter-text::-webkit-scrollbar-track {
            background: transparent;
        }
        .letter-text::-webkit-scrollbar-thumb {
            background: var(--heart-color);
            border-radius: 4px;
        }

        .letter-text h1 {
            font-size: 17px;
            color: var(--heart-color);
            margin-bottom: 12px;
            font-weight: 700;
        }

        .letter-text p {
            margin-bottom: 9px;
            font-weight: 300;
        }

        .letter-text p:last-of-type {
            margin-bottom: 0;
        }

        .signature {
            margin-top: 14px;
            font-weight: 500 !important;
            font-style: italic;
            color: var(--heart-color);
        }

        /* --- ПОДСКАЗКА --- */
        .hint {
            position: absolute;
            bottom: -40px;
            left: 0;
            width: 100%;
            text-align: center;
            color: var(--heart-color);
            font-size: 14px;
            font-weight: 500;
            animation: pulse 1.5s infinite;
            transition: opacity 0.3s ease;
            pointer-events: none;
        }

        @keyframes pulse {
            0%   { transform: scale(1);    opacity: 0.8; }
            50%  { transform: scale(1.05); opacity: 1;   }
            100% { transform: scale(1);    opacity: 0.8; }
        }

        /* --- СОСТОЯНИЕ ОТКРЫТИЯ --- */
        .wrapper.open .flap {
            transform: rotateX(180deg);
            z-index: 1;
            border-color: var(--envelope-color) transparent transparent transparent;
        }

        .wrapper.open .heart {
            transform: rotate(-45deg) scale(0);
            opacity: 0;
            animation: none;
        }

        .wrapper.open .letter {
            transform: translateY(-160px);
            height: 360px;
            z-index: 4;
            box-shadow: 0 20px 40px rgba(0,0,0,0.15);
        }

        .wrapper.open .letter-text {
            opacity: 1;
            transform: translateY(0);
        }

        .wrapper.open .hint {
            opacity: 0;
        }

        /* --- АДАПТИВ --- */
        @media (max-width: 400px) {
            .envelope {
                transform: scale(0.88);
                transform-origin: center;
            }
            .letter-text { font-size: 12.5px; }
        }

        @media (max-height: 620px) {
            .envelope { transform: scale(0.9); }
            .letter-text { font-size: 12.5px; }
        }

        /* --- УВАЖЕНИЕ К НАСТРОЙКАМ ПОЛЬЗОВАТЕЛЯ --- */
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

    <div class="wrapper"
         id="envelopeWrapper"
         role="button"
         tabindex="0"
         aria-label="Открыть письмо"
         aria-expanded="false">
        <div class="flap"></div>
        <div class="heart"></div>

        <div class="envelope">
            <div class="letter">
                <div class="letter-text">
                    <h1>Привет, любимая! ❤️</h1>
                    <p>Решил написать тебе, потому что в коротких сообщениях сложно передать всё, что чувствую.</p>
                    <p>Знаешь, я часто думаю о том, как мне с тобой повезло. С твоим появлением в моей жизни стало больше тепла, света и радости.</p>
                    <p>Мне очень нравится проводить с тобой время: говорить обо всём и ни о чём, смеяться до слёз или просто молчать рядом — и в этом молчании тоже есть что-то особенное.</p>
                    <p>С тобой мне легко и спокойно. Ты удивительная — с твоим характером, улыбкой и той самой энергетикой, которая делает каждый день ярче.</p>
                    <p>Спасибо тебе за поддержку, нежность и за то, что ты просто есть. Я тебя очень люблю и очень ценю.</p>
                    <p class="signature">Твой навеки ✨</p>
                </div>
            </div>
        </div>
        <div class="hint">Нажми, чтобы открыть ✨</div>
    </div>

    <script>
        (function () {
            'use strict';

            const wrapper = document.getElementById('envelopeWrapper');

            function toggleEnvelope() {
                const isOpen = wrapper.classList.toggle('open');
                wrapper.setAttribute('aria-expanded', String(isOpen));
            }

            wrapper.addEventListener('click', toggleEnvelope);
            wrapper.addEventListener('keydown', function (e) {
                if (e.key === 'Enter' || e.key === ' ' || e.key === 'Spacebar') {
                    e.preventDefault();
                    toggleEnvelope();
                }
            });

            // Генератор падающих сердечек
            function createFallingHearts() {
                const bg = document.getElementById('heartsBg');
                const symbols = ['❤️', '💖', '💕', '🌸', '✨', '💗'];
                const maxHearts = 22;
                const fragment = document.createDocumentFragment();

                for (let i = 0; i < maxHearts; i++) {
                    const heart = document.createElement('div');
                    heart.classList.add('falling-heart');
                    heart.textContent = symbols[Math.floor(Math.random() * symbols.length)];
                    heart.style.left = (Math.random() * 100).toFixed(2) + 'vw';
                    heart.style.animationDuration = (Math.random() * 4 + 5).toFixed(2) + 's';
                    heart.style.animationDelay = (Math.random() * 6).toFixed(2) + 's';
                    heart.style.fontSize = (Math.random() * 15 + 14).toFixed(1) + 'px';
                    fragment.appendChild(heart);
                }

                bg.appendChild(fragment);
            }

            if (document.readyState === 'loading') {
                document.addEventListener('DOMContentLoaded', createFallingHearts);
            } else {
                createFallingHearts();
            }
        })();
    </script>

</body>
</html>
