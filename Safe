<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SafeSpace | Instant Intervention</title>
    <style>
        :root {
            --bg: #0a192f;
            --card: #112240;
            --teal: #64ffda;
            --red: #ff4d4d;
            --gold: #ffd700;
            --text: #ccd6f6;
        }

        body { 
            background: var(--bg); 
            color: var(--text); 
            font-family: sans-serif; 
            margin: 0; 
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        .screen { display: none; flex-direction: column; align-items: center; justify-content: center; padding: 20px; text-align: center; min-height: 80vh; }
        .active { display: flex; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .btn { 
            background: var(--card); 
            border: 1px solid var(--teal); 
            color: var(--teal); 
            padding: 15px 25px; 
            border-radius: 30px; 
            cursor: pointer; 
            margin: 10px; 
            width: 250px; 
            font-weight: bold;
            transition: 0.2s;
        }
        .btn-sos { background: var(--red); color: white; border: none; font-size: 1.2rem; }
        .btn-gold { border-color: var(--gold); color: var(--gold); }

        /* BREATHING ANIMATION */
        .breathe-circle { 
            width: 150px; height: 150px; 
            background: var(--teal); 
            border-radius: 50%; 
            opacity: 0.3; 
            animation: breathe 12s infinite ease-in-out; 
        }
        @keyframes breathe { 
            0%, 100% { transform: scale(0.8); opacity: 0.2; } 
            40%, 60% { transform: scale(1.4); opacity: 0.5; } 
        }

        nav { 
            position: sticky; bottom: 0; width: 100%; 
            background: var(--card); display: flex; 
            justify-content: space-around; padding: 15px 0;
            border-top: 1px solid rgba(100, 255, 218, 0.1);
        }
        nav button { background: none; border: none; color: var(--text); cursor: pointer; opacity: 0.7; }

        #tutorial-overlay {
            position: fixed; inset: 0; background: var(--bg); z-index: 1000;
            display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 40px;
        }
    </style>
</head>
<body>

    <div id="tutorial-overlay">
        <h1 style="color: var(--teal);">SafeSpace</h1>
        <p>This is your digital weighted blanket.</p>
        <div style="text-align: left; margin: 20px 0;">
            <p>🔴 <strong>SOS:</strong> Immediate panic help.</p>
            <p>❄️ <strong>Reset:</strong> Physical "Dive Reflex" fix.</p>
            <p>🧠 <strong>CBT:</strong> Fact-check anxious thoughts.</p>
        </div>
        <button class="btn" onclick="closeTutorial()">Start Healing</button>
    </div>

    <div id="home" class="screen active">
        <h1>Hello, Joe.</h1>
        <p>How does your nervous system feel?</p>
        <button class="btn btn-sos" onclick="show('sos')">SOS: I'M PANICKING</button>
        <button class="btn" onclick="show('grounding')">5-4-3-2-1 Grounding</button>
        <button class="btn" onclick="show('icedive')">Emergency Ice Reset ❄️</button>
        <button class="btn" onclick="show('cbt')">Thought Fact-Checker</button>
    </div>

    <div id="sos" class="screen">
        <div class="breathe-circle"></div>
        <h2 id="b-text">Breathe In...</h2>
        <p>Follow the circle's expansion.</p>
        <button class="btn" onclick="show('home')">I'm calmer now</button>
    </div>

    <div id="grounding" class="screen">
        <h2 id="g-title">Grounding</h2>
        <p id="g-desc" style="font-size: 1.3rem; color: var(--teal);">Name 5 things you can SEE.</p>
        <h1 id="g-count">5</h1>
        <button class="btn" onclick="nextStep()">Next Sense</button>
    </div>

    <div id="icedive" class="screen">
        <h2 style="color: #00f2ff;">System Reset</h2>
        <p>Splash your face with ice water or hold an ice cube for 15 seconds.</p>
        <h1 id="timer">15</h1>
        <button class="btn" onclick="startIceTimer()">Start Timer</button>
        <button class="btn" onclick="show('home')" style="border:none; opacity:0.5;">Cancel</button>
    </div>

    <div id="cbt" class="screen">
        <h2>Fact-Checker</h2>
        <textarea id="thought" placeholder="What is the anxious thought?" style="width:80%; height:80px; padding:10px; border-radius:10px;"></textarea>
        <button class="btn btn-gold" onclick="triggerVault()">Analyze & Store</button>
        <button class="btn" onclick="show('home')">Back</button>
    </div>

    <nav>
        <button onclick="show('home')">HOME</button>
        <button onclick="show('sos')">SOS</button>
        <button onclick="triggerVault()">VAULT 🔒</button>
    </nav>

    <script>
        // NAVIGATION
        function show(id) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            if(id === 'sos') startBreathingText();
        }

        function closeTutorial() {
            document.getElementById('tutorial-overlay').style.display = 'none';
            localStorage.setItem('safespace_user', 'true');
        }

        // SOS TEXT LOGIC
        function startBreathingText() {
            const txt = document.getElementById('b-text');
            setInterval(() => {
                let s = new Date().getSeconds() % 12;
                if (s < 5) txt.innerText = "Breathe In...";
                else if (s < 7) txt.innerText = "Hold...";
                else txt.innerText = "Breathe Out...";
            }, 1000);
        }

        // GROUNDING LOGIC
        let step = 5;
        const prompts = ["SEE", "TOUCH", "HEAR", "SMELL", "TASTE"];
        function nextStep() {
            step--;
            if(step < 1) { show('home'); step = 5; }
            document.getElementById('g-desc').innerText = "Name " + step + " things you can " + prompts[5-step] + ".";
            document.getElementById('g-count').innerText = step;
        }

        // ICE TIMER
        function startIceTimer() {
            let t = 15;
            const el = document.getElementById('timer');
            const interval = setInterval(() => {
                t--; el.innerText = t;
                if(t <= 0) { clearInterval(interval); el.innerText = "DONE"; alert("Vagus Nerve Reset Complete."); }
            }, 1000);
        }

        // VAULT (UPSELL)
        function triggerVault() {
            const email = prompt("SafeSpace Pro: Enter email to unlock the Resilience Vault & save your data ($4.99/mo):");
            if(email) alert("Redirecting " + email + " to secure payment...");
        }

        window.onload = () => {
            if(localStorage.getItem('safespace_user')) document.getElementById('tutorial-overlay').style.display = 'none';
        }
    </script>
</body>
</html>
