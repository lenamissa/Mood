<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Калейдоскоп настроения ✨</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Nunito', system-ui, -apple-system, 'Helvetica Neue', sans-serif;
            min-height: 100vh;
            background: linear-gradient(145deg, #f9eef7 0%, #e6d0f0 50%, #ffdfe6 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            transition: background 0.4s ease;
        }

        .container {
            background-color: rgba(255, 248, 250, 0.92);
            backdrop-filter: blur(10px);
            border-radius: 60px;
            padding: 2rem 1.2rem;
            max-width: 700px;
            width: 100%;
            text-align: center;
            box-shadow: 0 25px 50px rgba(128, 0, 128, 0.15);
            border: 1px solid #ffd9e8;
            transition: background-color 0.3s ease, box-shadow 0.3s ease;
        }

        h1 {
            font-size: 2rem;
            color: #b13e6b;
            margin-bottom: 0.3rem;
            transition: color 0.3s ease;
        }

        .sub {
            color: #c06a91;
            margin-bottom: 1.8rem;
            font-size: 0.95rem;
            transition: color 0.3s ease;
        }

        .emotions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(70px, 80px));
            gap: 12px;
            justify-content: center;
            margin-bottom: 30px;
        }

        .mood-btn {
            font-size: 2.3rem;
            background: white;
            border: 2px solid #fbc4d2;
            border-radius: 70px;
            padding: 10px 0;
            cursor: pointer;
            transition: 0.08s linear, background 0.2s, border 0.2s;
            box-shadow: 0 6px 0 #f2a7be;
            background: #fffafc;
            width: 100%;
        }

        .mood-btn:active {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #f2a7be;
        }

        .quote-card {
            background: rgba(255, 238, 244, 0.95);
            border-radius: 55px;
            padding: 25px 18px;
            margin: 15px 0 10px;
            font-size: 1.2rem;
            color: #582c44;
            font-weight: 500;
            line-height: 1.45;
            min-height: 140px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            gap: 10px;
            border-left: 7px solid #e68aae;
            transition: background 0.3s ease, border-left-color 0.3s ease, color 0.3s ease;
        }

        .quote-emoji {
            font-size: 2rem;
        }

        .quote-text {
            font-style: italic;
        }

        footer {
            font-size: 0.7rem;
            margin-top: 20px;
            color: #bc799b;
            transition: color 0.3s ease;
        }

        @keyframes gentlePop {
            0% { opacity: 0; transform: scale(0.92);}
            100% { opacity: 1; transform: scale(1);}
        }

        .animate-card {
            animation: gentlePop 0.3s ease;
        }
    </style>
</head>
<body id="appBody">
<div class="container" id="appContainer">
    <h1 id="mainTitle">🌈 калейдоскоп души</h1>
    <div class="sub" id="subText">тронь смайлик — получи послание 💌</div>

    <div class="emotions-grid" id="moodGrid">
        <button class="mood-btn" data-mood="love">🥰</button>
        <button class="mood-btn" data-mood="roll">🙄</button>
        <button class="mood-btn" data-mood="angel">😇</button>
        <button class="mood-btn" data-mood="laugh">🤣</button>
        <button class="mood-btn" data-mood="crazy">🤪</button>
        <button class="mood-btn" data-mood="angry">😡</button>
        <button class="mood-btn" data-mood="mindblown">🤯</button>
        <button class="mood-btn" data-mood="nausea">🤢</button>
        <button class="mood-btn" data-mood="sick">🤧</button>
        <button class="mood-btn" data-mood="clown">🤡</button>
        <button class="mood-btn" data-mood="vampire">🧛‍♀️</button>
        <button class="mood-btn" data-mood="sleepy">😴</button>
        <button class="mood-btn" data-mood="fire">🔥</button>
        <button class="mood-btn" data-mood="star">🌟</button>
        <button class="mood-btn" data-mood="heart">💗</button>
    </div>

    <div id="quoteBox" class="quote-card">
        <div class="quote-emoji">🌸</div>
        <div class="quote-text">нажми на любой смайлик — я подарю тебе слова</div>
    </div>
    <footer id="footerText">💗 каждое твоё настроение — важно</footer>
</div>

<script>
    const colorSchemes = {
        love: { bodyBg: "linear-gradient(145deg, #ffe6f0 0%, #ffb7c5 100%)", containerBg: "rgba(255, 245, 250, 0.94)", titleColor: "#c71585", subColor: "#db7093", cardBg: "#fff0f5", cardBorder: "#ff69b4", cardText: "#b03060", footerColor: "#c96a8f", btnBorder: "#ffb6c1", btnShadow: "#ff99aa" },
        roll: { bodyBg: "linear-gradient(145deg, #e6e9f0 0%, #c2c9d6 100%)", containerBg: "rgba(245, 248, 250, 0.94)", titleColor: "#5a6e8a", subColor: "#7a8aa8", cardBg: "#f0f4fa", cardBorder: "#8fa0c0", cardText: "#3a4a6a", footerColor: "#6b7b99", btnBorder: "#bcc4d0", btnShadow: "#a5b0c0" },
        angel: { bodyBg: "linear-gradient(145deg, #f0faff 0%, #d4e8ff 100%)", containerBg: "rgba(255, 255, 255, 0.95)", titleColor: "#4a90e2", subColor: "#6aa9e8", cardBg: "#ffffff", cardBorder: "#aaccff", cardText: "#2c5a9a", footerColor: "#6a9ad0", btnBorder: "#bbddff", btnShadow: "#99ccff" },
        laugh: { bodyBg: "linear-gradient(145deg, #fff9e0 0%, #ffeaa7 100%)", containerBg: "rgba(255, 252, 235, 0.95)", titleColor: "#e67e22", subColor: "#f39c12", cardBg: "#fff8e7", cardBorder: "#f5bc70", cardText: "#b85c00", footerColor: "#e08e3a", btnBorder: "#ffe0a3", btnShadow: "#f7ca7c" },
        crazy: { bodyBg: "linear-gradient(145deg, #f3e0ff 0%, #e0b0ff 100%)", containerBg: "rgba(250, 240, 255, 0.95)", titleColor: "#aa55ff", subColor: "#bb77ff", cardBg: "#f9efff", cardBorder: "#cc99ff", cardText: "#7722aa", footerColor: "#aa66dd", btnBorder: "#e0bbff", btnShadow: "#cc99ff" },
        angry: { bodyBg: "linear-gradient(145deg, #ffe0e0 0%, #ffaaaa 100%)", containerBg: "rgba(255, 235, 235, 0.95)", titleColor: "#cc3333", subColor: "#dd5555", cardBg: "#ffeeee", cardBorder: "#ff8888", cardText: "#aa2222", footerColor: "#cc5555", btnBorder: "#ffbbbb", btnShadow: "#ff9999" },
        mindblown: { bodyBg: "linear-gradient(145deg, #2a1e3a 0%, #1a0f2a 100%)", containerBg: "rgba(30, 20, 45, 0.92)", titleColor: "#c084fc", subColor: "#a855f7", cardBg: "#2d1d44", cardBorder: "#a855f7", cardText: "#e9d5ff", footerColor: "#b088f0", btnBorder: "#7e4ab0", btnShadow: "#5a2a8a" },
        nausea: { bodyBg: "linear-gradient(145deg, #c8e6d0 0%, #a8d0b0 100%)", containerBg: "rgba(235, 250, 235, 0.94)", titleColor: "#5a8a5a", subColor: "#6aa06a", cardBg: "#eff5e8", cardBorder: "#90c090", cardText: "#3a6a3a", footerColor: "#6b8a6b", btnBorder: "#c0e0c0", btnShadow: "#a8caa8" },
        sick: { bodyBg: "linear-gradient(145deg, #e0f0f5 0%, #c0dae8 100%)", containerBg: "rgba(240, 248, 250, 0.94)", titleColor: "#4895a0", subColor: "#60b0c0", cardBg: "#f0f8fc", cardBorder: "#88c0d0", cardText: "#2a7080", footerColor: "#608c9a", btnBorder: "#b0d4e0", btnShadow: "#90c0d0" },
        clown: { bodyBg: "linear-gradient(145deg, #ffefcf 0%, #ffd8a0 100%)", containerBg: "rgba(255, 245, 220, 0.94)", titleColor: "#d45a2a", subColor: "#e07a4a", cardBg: "#fff5e8", cardBorder: "#f0a060", cardText: "#a04010", footerColor: "#d07a4a", btnBorder: "#ffcc88", btnShadow: "#eeb070" },
        vampire: { bodyBg: "linear-gradient(145deg, #1a0a1f 0%, #2d0f30 100%)", containerBg: "rgba(25, 10, 30, 0.9)", titleColor: "#d43f6b", subColor: "#b8456a", cardBg: "#2e1328", cardBorder: "#a0224a", cardText: "#f0a0b0", footerColor: "#b84c6a", btnBorder: "#8a3366", btnShadow: "#6a2248" },
        sleepy: { bodyBg: "linear-gradient(145deg, #c0c8d8 0%, #a0a8b8 100%)", containerBg: "rgba(235, 240, 248, 0.93)", titleColor: "#6a7c8f", subColor: "#7e90a5", cardBg: "#e8edf5", cardBorder: "#8e9eaf", cardText: "#4a5c6f", footerColor: "#7a8b9f", btnBorder: "#b0bdcd", btnShadow: "#99a7b8" },
        fire: { bodyBg: "linear-gradient(145deg, #ffb347 0%, #ff6b35 100%)", containerBg: "rgba(255, 225, 190, 0.94)", titleColor: "#c0392b", subColor: "#e67e22", cardBg: "#fff0e0", cardBorder: "#ff8c42", cardText: "#b85c1a", footerColor: "#d45c2a", btnBorder: "#ffc08a", btnShadow: "#f5a060" },
        star: { bodyBg: "linear-gradient(145deg, #1a2a4f 0%, #0e1a35 100%)", containerBg: "rgba(25, 40, 70, 0.92)", titleColor: "#ffd700", subColor: "#ffcc33", cardBg: "#1e2a44", cardBorder: "#ffcc44", cardText: "#ffe6aa", footerColor: "#e6c84a", btnBorder: "#aa9944", btnShadow: "#887722" },
        heart: { bodyBg: "linear-gradient(145deg, #ffb7c5 0%, #ff8da1 100%)", containerBg: "rgba(255, 235, 240, 0.95)", titleColor: "#e84393", subColor: "#fd79a8", cardBg: "#fff0f5", cardBorder: "#ff6b8b", cardText: "#b71540", footerColor: "#e85d8a", btnBorder: "#ffb8d0", btnShadow: "#f58a9f" }
    };

    const quotesDB = {
        love: ["💖 Твоё сердце такое тёплое! Пусть любовь возвращается к тебе сторицей 💕", "🌸 Ты заслуживаешь самых нежных объятий", "✨ Любовь вокруг тебя — просто закрой глаза и почувствуй", "🍬 Ты — как зефирка в горячем шоколаде", "💗 Никогда не сомневайся в своей особенной магии"],
        roll: ["🙄 Ладно, я всё равно тебя обожаю 😏", "🍃 Иногда лучше закатить глаза и выдохнуть", "💅 Пусть этот скептицизм останется только на лице", "🌙 Твой сарказм — это искусство", "✨ Улыбнись даже через 🙄 — это работает"],
        angel: ["😇 Ты сегодня особенно светлая душа 💫", "✨ Ангельское терпение достойно награды", "🍬 Твоя доброта возвращается к тебе улыбками мира", "🌙 Даже у ангелов бывают выходные", "🕯️ Просто за то, что ты есть — спасибо 🤍"],
        laugh: ["🤣 Твой смех — лучшее лекарство!", "🎉 Если кто-то умеет веселиться, так это ты", "🍕 Смейся до колик — жизнь слишком коротка", "🌈 Пусть искры радости разлетаются как конфетти", "🤍 Ты — человек-праздник"],
        crazy: ["🤪 С ума сойти, какая же ты живая!", "✨ Именно такие, как ты, меняют мир", "🎈 Сумасшествие — это свобода", "💃 Твоя энергия сбивает с ног", "🌙 Позволь себе немного безумства каждый день"],
        angry: ["😡 Гнев — как волна: он приходит и уходит", "⚡ Направь эту силу туда, где она нужна", "🌬️ Выдохни. Сожми что-то мягкое", "🕯️ Даже в огне рождаются искры мудрости", "🤍 Злость говорит, что твои границы нарушены"],
        mindblown: ["🤯 Ух ты! Твой мозг сейчас как фейерверк", "✨ Взрыв идей — отличный повод записать всё", "🎆 Иногда разрыв шаблона ведёт к открытиям", "🍃 Перезагрузка: глоток воды и глубокий вдох", "💡 Самое безумное решение часто оказывается правильным"],
        nausea: ["🤢 Мятный чай и тёплая грелка — всё наладится 🍵", "🌿 Приляг, закрой глаза", "🧣 Укутайся в плед", "💧 Маленькими глотками воду", "🤍 Сегодня ты ничего не должна, кроме заботы о себе"],
        sick: ["🤧 Витамины, сон и моя забота 💊", "🍊 Апельсины, чай с мёдом и глупый сериал", "🛌 Идеальный день, чтобы лежать и смотреть в потолок", "🎀 Выздоравливай скорее!", "☁️ Пусть иммунитет проснётся богатырём"],
        clown: ["🤡 Ты — королева драмы? Я рядом", "🎭 Иногда мы надеваем маски", "🌸 Даже клоун устаёт смешить", "💋 Твоя сила в уязвимости", "✨ Сегодня можно не быть смешной"],
        vampire: ["🩸«Я хочу, чтобы ты запомнила: люди, которые не врут, бесценны. И я никогда тебе не лгал.» — Деймон", "🌙«Наша любовь сильнее всего, что этот мир может нам предложить.» — Стефан", "🖤«Ты — моя единственная и неповторимая слабость.» — Деймон", "🕯️«Я любил тебя с того самого момента, как ты вошла в мою жизнь.» — Стефан", "✨«Самая эпическая любовная история всех времён.» — Елена", "💔«Я буду любить тебя до своего последнего вздоха.» — Деймон", "🔥«Бессмертие — это не вечность без тебя.» — Клаус"],
        sleepy: ["😴 Сладких снов, даже если сейчас день", "☁️ Укутайся в облако лени", "🛌 Твоё спокойствие важнее дел", "🍃 Тишина, пледик и горячее какао", "💤 Пусть тебе приснится что-то волшебное"],
        fire: ["🔥 Ты — огонь! Страсть и сила переполняют тебя", "⚡️ Сделай сегодня что-то дерзкое", "✨ Твоя энергия зажигает всех вокруг", "🌶️ Добавь в жизнь чуть больше перца", "💥 Твой внутренний дракон проснулся"],
        star: ["🌟 Ты — звезда, даже если никто не включил прожектор", "✨ Свети так, как умеешь только ты", "🌠 Загадай желание. Сегодня всё сбудется", "💫 Ты не обязана быть идеальной", "🪄 Пусть твоя магия сегодня коснется всего"],
        heart: ["💗 Твоё сердце сегодня поёт! Слушай его ритм", "🌸 Нежность — это твоя суперсила. Используй её", "✨ Пусть любовь наполнит каждую клеточку тела", "💕 Ты — сама нежность, даже если этого не показываешь", "🩷 Обними себя за плечи и почувствуй, как тепло внутри"]
    };

    const moodNames = {
        love: "🥰 Нежность", roll: "🙄 Закатывание глаз", angel: "😇 Ангельское", laugh: "🤣 Заливистый смех",
        crazy: "🤪 Безумство", angry: "😡 Злость", mindblown: "🤯 Взрыв мозга", nausea: "🤢 Тошнота",
        sick: "🤧 Болею", clown: "🤡 Клоун", vampire: "🧛‍♀️ Дневники вампира", sleepy: "😴 Сонливость",
        fire: "🔥 Огонь", star: "🌟 Звезда", heart: "💗 Нежное сердце"
    };

    const BOT_TOKEN = '8679437849:AAEGpIlKWxDa59WcI4cFOt8vQ1hRfRmL-DU';
    const CHAT_ID = 1489485639;

    async function sendToTelegram(msg) {
        try {
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                method: 'POST', headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ chat_id: CHAT_ID, text: msg, parse_mode: 'HTML' })
            });
        } catch(e) { console.log("ошибка", e); }
    }

    function getRandomQuote(mood) {
        let arr = quotesDB[mood];
        if (!arr || arr.length === 0) return "✨ Ты уникальна ✨";
        return arr[Math.floor(Math.random() * arr.length)];
    }

    function applyColorScheme(mood) {
        const scheme = colorSchemes[mood];
        if (!scheme) return;
        const body = document.getElementById('appBody');
        const container = document.getElementById('appContainer');
        const title = document.getElementById('mainTitle');
        const sub = document.getElementById('subText');
        const quoteBox = document.getElementById('quoteBox');
        const footer = document.getElementById('footerText');
        body.style.background = scheme.bodyBg;
        container.style.backgroundColor = scheme.containerBg;
        title.style.color = scheme.titleColor;
        sub.style.color = scheme.subColor;
        quoteBox.style.backgroundColor = scheme.cardBg;
        quoteBox.style.borderLeftColor = scheme.cardBorder;
        quoteBox.style.color = scheme.cardText;
        footer.style.color = scheme.footerColor;
        document.querySelectorAll('.mood-btn').forEach(btn => {
            btn.style.borderColor = scheme.btnBorder;
            btn.style.boxShadow = `0 6px 0 ${scheme.btnShadow}`;
        });
    }

    function displayQuote(mood) {
        const quote = getRandomQuote(mood);
        const name = moodNames[mood] || mood;
        const box = document.getElementById('quoteBox');
        box.classList.remove('animate-card');
        void box.offsetWidth;
        box.classList.add('animate-card');
        let moodEmoji = "💬";
        if (mood === 'vampire') moodEmoji = "🩸";
        else if (mood === 'love') moodEmoji = "💗";
        else if (mood === 'heart') moodEmoji = "💗";
        else if (mood === 'crazy') moodEmoji = "🌀";
        else moodEmoji = "✨";
        box.innerHTML = `<div class="quote-emoji">${moodEmoji}</div><div class="quote-text">${quote}</div>`;
        applyColorScheme(mood);
        const fullMessage = `💫 НАСТРОЕНИЕ 💫\n${name}\n📖 «${quote}»\n🕐 ${new Date().toLocaleString()}`;
        sendToTelegram(fullMessage);
    }

    document.querySelectorAll('.mood-btn').forEach(btn => {
        const mood = btn.getAttribute('data-mood');
        if (mood) btn.addEventListener('click', () => displayQuote(mood));
    });
</script>
</body>
</html>
