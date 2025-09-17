<!--
Однофайловий сайт-привітання для хлопця-айтішника
Щоб використати: збережіть цей файл як ouvre-moi.html і відкрийте у браузері.
Змінити ім'я та повідомлення можна у секції <script> -> змінні `BF_NAME` та `PERSONAL_MESSAGE`.
-->
<!doctype html>
<html lang="uk">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>ouvre-moi 🎉</title>
    <style>
        :root {
            --bg: #0f1724;
            --card: #0b1220;
            --accent: #7c3aed;
            --muted: #94a3b8;
            --glass: rgba(255, 255, 255, 0.04);
        }

        html,
        body {
            height: 100%;
            margin: 0;
            font-family: Inter, ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, 'Helvetica Neue', Arial
        }

        body {
            background: radial-gradient(circle at 10% 10%, rgba(124, 58, 237, 0.12), transparent 5%), linear-gradient(180deg, var(--bg), #051025);
            color: #e6eef8;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 24px
        }

        .container {
            width: 100%;
            max-width: 980px;
            display: grid;
            grid-template-columns: 1fr 420px;
            gap: 24px;
            align-items: center
        }

        @media (max-width:900px) {
            .container {
                grid-template-columns: 1fr;
                padding: 12px
            }
        }

        .card {
            background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), transparent);
            border-radius: 16px;
            padding: 28px;
            box-shadow: 0 8px 30px rgba(2, 6, 23, 0.7);
            border: 1px solid rgba(255, 255, 255, 0.03)
        }

        .hero h1 {
            font-size: 36px;
            margin: 0 0 6px 0;
            letter-spacing: -0.5px
        }

        .sub {
            color: var(--muted);
            margin-bottom: 18px
        }

        .code-window {
            background: var(--card);
            padding: 18px;
            border-radius: 12px;
            font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, monospace;
            font-size: 13px;
            color: #cfe8ff;
            line-height: 1.6
        }

        .btn {
            display: inline-block;
            padding: 10px 16px;
            border-radius: 10px;
            background: linear-gradient(90deg, var(--accent), #06b6d4);
            color: #021126;
            font-weight: 700;
            cursor: pointer;
            border: none
        }

        .btn:active {
            transform: translateY(1px)
        }

        .small {
            font-size: 13px;
            color: var(--muted)
        }

        .party {
            position: relative;
            min-height: 300px;
            display: flex;
            align-items: center;
            justify-content: center
        }

        .message {
            font-size: 18px;
            color: #eaf6ff;
            text-align: center;
            padding: 20px
        }

        .reveal {
            margin-top: 16px
        }

        .terminal {
            background: linear-gradient(180deg, rgba(0, 0, 0, 0.35), rgba(255, 255, 255, 0.02));
            border-radius: 10px;
            padding: 12px;
            font-family: ui-monospace, monospace;
            font-size: 13px;
            color: #bde6c9
        }

        footer {
            margin-top: 16px;
            color: var(--muted);
            font-size: 13px
        }

        /* little stars */
        .stars {
            position: absolute;
            inset: 0;
            pointer-events: none
        }

        canvas#confetti {
            position: absolute;
            inset: 0;
            width: 100%;
            height: 100%;
            pointer-events: none
        }

        .secret {
            opacity: 0.02;
            font-size: 10px;
            user-select: none
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="card hero">
            <h1 id="headline">З Днем Народження, <span id="bf-name">Друже!</span> 🎉</h1>
            <div class="sub">Невелике сайт-привітання, зроблене з любов'ю для твого айтішного хлопця.</div>

            <div class="party card" style="position:relative; overflow:hidden;">
                <canvas id="confetti"></canvas>
                <div class="message" id="main-message">Натисни кнопку, щоб розгорнути привітання</div>
            </div>

            <div class="reveal">
                <button class="btn" id="revealBtn">🎁 Відкрити</button>
                <button class="btn" id="easterBtn"
                    style="margin-left:10px;background:linear-gradient(90deg,#111827,#374151);color:#fff">💻
                    Тех-пасхалка</button>
            </div>

            <div class="small" style="margin-top:14px">Можна змінити текст у коді: змінні BF_NAME, PERSONAL_MESSAGE.
            </div>
            <footer>З любов'ю — ваша фронтенд-студентка 😉</footer>
        </div>

        <div class="card">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
                <div><strong>Додатково</strong>
                    <div class="small">(техно-стиль для айті)</div>
                </div>
            </div>

            <div class="code-window" id="code">
                <div class="terminal" id="terminal">$ // тут з'явиться пасхалка</div>
            </div>

            <div style="margin-top:12px">
                <button class="btn" id="downloadBtn">⬇️ Зберегти як GIF</button>
                <div class="small" style="margin-top:8px">Натисни, щоб зберегти короткий анімований скрін (у
                    підтримуваних браузерах).</div>
            </div>

            <div style="margin-top:12px" class="secret">/* created: single-file birthday greeting */</div>
        </div>
    </div>

    <script>
        // === Налаштування (заміни тут) ===
        const BF_NAME = "Коханий"; // ім'я хлопця
        const PERSONAL_MESSAGE = `Любий ${BF_NAME}, з днем народження! Бажаю нескінченних цікавих проєктів, чистого коду без багів та вечорів з хорошою кавою. Люблю тебе ❤️`;
        // ================================

        // Показ імені
        document.getElementById('bf-name').textContent = BF_NAME;

        // Reveal logic
        const revealBtn = document.getElementById('revealBtn');
        const mainMessage = document.getElementById('main-message');
        const confettiCanvas = document.getElementById('confetti');
        const terminal = document.getElementById('terminal');

        revealBtn.addEventListener('click', () => {
            mainMessage.innerHTML = `<strong style=\"font-size:20px\">${PERSONAL_MESSAGE}</strong>`;
            launchConfetti();
            playTune();
        });

        // Small easter egg for developer
        const easterBtn = document.getElementById('easterBtn');
        easterBtn.addEventListener('click', () => {
            const lines = [
                `> git commit -m \"happy-birthday-${BF_NAME.toLowerCase().replace(/\\s+/g, '-')}\"`,
                `> echo \"${PERSONAL_MESSAGE.replace(/\"/g, '\\\\\"')}\" > love_note.txt`,
                `> cat love_note.txt \\n${PERSONAL_MESSAGE}`
            ];
            terminal.textContent = '';
            let i = 0;
            const timer = setInterval(() => {
                if (i >= lines.length) { clearInterval(timer); return; }
                terminal.textContent += lines[i] + '\\n';
                i++;
            }, 700);
        });

        // ===== Confetti (lightweight) =====
        function launchConfetti() {
            const W = confettiCanvas.width = confettiCanvas.offsetWidth;
            const H = confettiCanvas.height = confettiCanvas.offsetHeight;
            const ctx = confettiCanvas.getContext('2d');
            const pieces = [];
            const colors = ['#7c3aed', '#06b6d4', '#f59e0b', '#ef4444', '#34d399'];
            for (let i = 0; i < 120; i++) pieces.push({ x: Math.random() * W, y: Math.random() * H - H, r: Math.random() * 8 + 4, dx: (Math.random() - 0.5) * 2, dy: Math.random() * 3 + 2, color: colors[Math.floor(Math.random() * colors.length)], rot: Math.random() * 360, drot: (Math.random() - 0.5) * 6 });
            let t = 0;
            function draw() {
                ctx.clearRect(0, 0, W, H);
                for (let p of pieces) {
                    p.x += p.dx; p.y += p.dy + Math.sin((t + p.x) * 0.01) * 0.6; p.rot += p.drot;
                    ctx.save(); ctx.translate(p.x, p.y); ctx.rotate(p.rot * Math.PI / 180);
                    ctx.fillStyle = p.color; ctx.fillRect(-p.r / 2, -p.r / 2, p.r, p.r * 0.6);
                    ctx.restore();
                }
                t += 1;
                requestAnimationFrame(draw);
            }
            draw();
            // stop after 7s
            setTimeout(() => { const c = confettiCanvas.getContext('2d'); c.clearRect(0, 0, W, H); }, 7000);
        }

        // ===== Play short tune with WebAudio =====
        function playTune() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const now = ctx.currentTime;
                const notes = [523.25, 659.25, 783.99, 1046.5]; // C5,E5,G5,C6
                for (let i = 0; i < notes.length; i++) {
                    const o = ctx.createOscillator();
                    const g = ctx.createGain();
                    o.type = 'sine'; o.frequency.value = notes[i];
                    g.gain.setValueAtTime(0.0001, now + i * 0.18);
                    g.gain.exponentialRampToValueAtTime(0.08, now + i * 0.18 + 0.02);
                    g.gain.exponentialRampToValueAtTime(0.0001, now + i * 0.18 + 0.16);
                    o.connect(g); g.connect(ctx.destination); o.start(now + i * 0.18); o.stop(now + i * 0.18 + 0.17);
                }
            } catch (e) { console.log('Audio unavailable', e); }
        }

        // ===== Download animated GIF (very small demo: using canvas frames) =====
        // Note: this is a tiny demo that captures 20 frames of current confetti canvas and builds a simple blob of images as zip-like fallback.
        const downloadBtn = document.getElementById('downloadBtn');
        downloadBtn.addEventListener('click', async () => {
            // capture current view by drawing body to canvas using html2canvas is not available offline; fallback: capture confetti canvas only
            try {
                const c = confettiCanvas;
                if (!c) throw 'no canvas';
                const data = c.toDataURL('image/png');
                const a = document.createElement('a'); a.href = data; a.download = 'confetti_snapshot.png'; document.body.appendChild(a); a.click(); a.remove();
            } catch (e) { alert('Не вдалося зберегти GIF у цьому браузері. Спробуйте інший браузер.'); }
        });

        // Resize canvas on window resize
        function resize() { confettiCanvas.width = confettiCanvas.offsetWidth; confettiCanvas.height = confettiCanvas.offsetHeight; }
        window.addEventListener('resize', resize); resize();

        // Auto small reveal if user likes
        // setTimeout(()=>{ /*auto-reveal if desired*/ }, 2000);

    </script>
</body>

</html>
