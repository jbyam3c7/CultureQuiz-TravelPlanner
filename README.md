<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cultural Match Assessment - Find Your Place in the World</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            max-width: 800px;
            width: 100%;
            padding: 40px;
            transform: translateY(0);
            transition: all 0.3s ease;
        }
        h1 {
            color: #333;
            text-align: center;
            margin-bottom: 10px;
            font-size: 2.5em;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 30px;
            font-size: 1.1em;
        }
        .progress-bar {
            height: 8px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 30px;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.3s ease;
        }
        .timer-container {
            margin: 20px 0;
            text-align: center;
            padding: 15px;
            background: #fff3cd;
            border-radius: 10px;
            border: 2px solid #ffc107;
        }
        .timer-bar {
            height: 15px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px 0;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        .timer-fill {
            height: 100%;
            background: linear-gradient(90deg, #28a745, #20c997);
            width: 100%;
            transition: width 1s linear;
        }
        .timer-fill.warning {
            background: linear-gradient(90deg, #ffc107, #ff9800);
        }
        .timer-fill.danger {
            background: linear-gradient(90deg, #dc3545, #c82333);
        }
        .timer-text {
            font-size: 1.5em;
            font-weight: bold;
            color: #333;
        }
        .timer-text.danger {
            color: #dc3545;
            animation: pulse 0.5s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        .question-container {
            display: none;
            animation: fadeIn 0.3s ease;
        }
        .question-container.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }
        .question {
            font-size: 1.3em;
            color: #333;
            margin-bottom: 25px;
            font-weight: 500;
        }
        .options {
            display: grid;
            gap: 12px;
        }
        .option {
            padding: 15px 20px;
            background: #f8f9fa;
            border: 2px solid transparent;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 1.05em;
        }
        .option:hover {
            background: #e8e9ff;
            border-color: #667eea;
            transform: translateX(5px);
        }
        .option.selected {
            background: #e8e9ff;
            border-color: #667eea;
        }
        .slider-container {
            margin: 20px 0;
        }
        .slider {
            width: 100%;
            height: 6px;
            border-radius: 5px;
            background: #e0e0e0;
            outline: none;
            -webkit-appearance: none;
        }
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: linear-gradient(135deg, #667eea, #764ba2);
            cursor: pointer;
        }
        .slider-labels {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 0.9em;
            color: #666;
        }
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }
        .nav-btn {
            padding: 12px 30px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 500;
            transition: transform 0.2s ease;
        }
        .nav-btn:hover {
            transform: scale(1.05);
        }
        .nav-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        #intro, #results, #timeout {
            text-align: center;
        }
        .start-btn {
            padding: 15px 40px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 1.2em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }
        .start-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
        }
        .timeout-message {
            text-align: center;
            padding: 40px;
            background: #ffe4e4;
            border-radius: 15px;
            margin: 20px 0;
        }
        .timeout-message h2 {
            color: #e74c3c;
            margin-bottom: 15px;
        }
        .result-card {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            margin: 20px 0;
            border-left: 5px solid;
            animation: slideIn 0.5s ease;
        }
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .match-percentage {
            font-size: 2em;
            font-weight: bold;
            color: #667eea;
            margin: 10px 0;
        }
        .country-name {
            font-size: 1.5em;
            font-weight: 600;
            color: #333;
            margin-bottom: 10px;
        }
        .cultural-traits {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid #dee2e6;
        }
        .trait {
            display: inline-block;
            background: white;
            padding: 6px 12px;
            border-radius: 20px;
            margin: 5px;
            font-size: 0.9em;
            color: #555;
        }
        .intro-text {
            color: #666;
            line-height: 1.6;
            margin: 20px 0;
        }
        .warning-text {
            color: #e74c3c;
            font-weight: bold;
            font-size: 1.1em;
            margin: 15px 0;
            padding: 15px;
            background: #ffe4e4;
            border-radius: 10px;
            border: 2px solid #e74c3c;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🌍 Cultural Match Assessment</h1>
        <p class="subtitle">Discover where in the world you truly belong</p>

        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>

        <div id="intro">
            <div class="intro-text">
                <p>This assessment analyzes your values, lifestyle preferences, social attitudes, and personality to find cultures where you'd naturally thrive.</p>
                <div class="warning-text">
                    ⏱️ IMPORTANT: You have 10 seconds to answer each question!<br>
                    The quiz will automatically restart if time runs out.<br>
                    This ensures authentic, instinctive responses.
                </div>
                <p>Answer honestly - there are no right or wrong answers, only what feels true to you.</p>
            </div>
            <button class="start-btn" id="startBtn">Begin Your Journey</button>
        </div>

        <div id="questionnaire" style="display: none;">
            <!-- Questions will be dynamically inserted here -->
        </div>

        <div id="timeout" style="display: none;">
            <div class="timeout-message">
                <h2>⏱️ Time's Up!</h2>
                <p>Not enough information collected. The quiz requires quick, instinctive responses.</p>
                <p>Please try again and answer within 10 seconds for each question.</p>
                <button class="start-btn" id="tryAgainBtn">Try Again</button>
            </div>
        </div>

        <div id="results" style="display: none;">
            <h2 style="color: #333; margin-bottom: 20px;">Your Cultural Matches</h2>
            <div id="resultsList"></div>
            <button class="start-btn" id="retakeBtn">Take Again</button>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "How do you prefer to handle conflict?",
                type: "multiple",
                options: [
                    { text: "Direct confrontation - address it immediately", value: "direct" },
                    { text: "Indirect communication - hint at issues diplomatically", value: "indirect" },
                    { text: "Avoid confrontation - maintain harmony at all costs", value: "harmony" },
                    { text: "Mediation - involve a neutral third party", value: "mediation" }
                ]
            },
            {
                question: "What's your ideal work-life balance?",
                type: "multiple",
                options: [
                    { text: "Work is life - I thrive on ambition and achievement", value: "work-focused" },
                    { text: "Clear separation - work to live, not live to work", value: "balanced" },
                    { text: "Life first - work should accommodate personal time", value: "life-focused" },
                    { text: "Flexible integration - blend work and life naturally", value: "integrated" }
                ]
            },
            {
                question: "How important is punctuality to you?",
                type: "slider",
                min: 1,
                max: 10,
                labels: ["Time is fluid", "Every minute counts"]
            },
            {
                question: "Your ideal social gathering involves:",
                type: "multiple",
                options: [
                    { text: "Large, lively parties with music and dancing", value: "festive" },
                    { text: "Intimate dinners with deep conversations", value: "intimate" },
                    { text: "Outdoor activities and adventures", value: "active" },
                    { text: "Quiet tea or coffee with one or two people", value: "minimal" }
                ]
            },
            {
                question: "How do you view family obligations?",
                type: "multiple",
                options: [
                    { text: "Family comes before everything else", value: "family-first" },
                    { text: "Important but shouldn't limit individual freedom", value: "balanced-family" },
                    { text: "Everyone should be independent", value: "independent" },
                    { text: "Extended family is as important as immediate family", value: "extended" }
                ]
            },
            {
                question: "Your preferred communication style is:",
                type: "multiple",
                options: [
                    { text: "Say exactly what you mean", value: "direct-comm" },
                    { text: "Use context and non-verbal cues", value: "contextual" },
                    { text: "Diplomatic and considerate of feelings", value: "diplomatic" },
                    { text: "Expressive with lots of emotion", value: "expressive" }
                ]
            },
            {
                question: "How much personal space do you need?",
                type: "slider",
                min: 1,
                max: 10,
                labels: ["Close contact is comforting", "Keep your distance"]
            },
            {
                question: "Your attitude toward rules and regulations:",
                type: "multiple",
                options: [
                    { text: "Rules exist for good reasons and should be followed", value: "rule-follower" },
                    { text: "Guidelines that can be bent when necessary", value: "flexible-rules" },
                    { text: "Often unnecessary restrictions on freedom", value: "rule-skeptic" },
                    { text: "Depends entirely on the situation", value: "situational" }
                ]
            },
            {
                question: "How do you prefer to eat meals?",
                type: "multiple",
                options: [
                    { text: "Long, social affairs with multiple courses", value: "social-dining" },
                    { text: "Quick and efficient", value: "efficient" },
                    { text: "Family-style sharing from common dishes", value: "communal" },
                    { text: "Individual portions, eat when hungry", value: "individual" }
                ]
            },
            {
                question: "Your ideal climate is:",
                type: "multiple",
                options: [
                    { text: "Hot and sunny year-round", value: "tropical" },
                    { text: "Four distinct seasons", value: "temperate" },
                    { text: "Cool and mild", value: "cool" },
                    { text: "Dry with minimal rain", value: "arid" }
                ]
            },
            {
                question: "How important is tradition to you?",
                type: "slider",
                min: 1,
                max: 10,
                labels: ["Innovation over tradition", "Preserve the old ways"]
            },
            {
                question: "Your approach to hierarchy and authority:",
                type: "multiple",
                options: [
                    { text: "Respect for authority is fundamental", value: "hierarchical" },
                    { text: "Everyone should be treated as equals", value: "egalitarian" },
                    { text: "Earned respect, not automatic", value: "meritocratic" },
                    { text: "Question authority when necessary", value: "questioning" }
                ]
            },
            {
                question: "Ideal spice level for your food?",
                type: "slider",
                min: 1,
                max: 10,
                labels: ["Bland is fine", "Bring the heat!"]
            },
            {
                question: "Your view on expressing emotions publicly:",
                type: "multiple",
                options: [
                    { text: "Express freely - emotions are natural", value: "expressive-emotions" },
                    { text: "Keep it controlled and appropriate", value: "controlled" },
                    { text: "Private matters should stay private", value: "private" },
                    { text: "Depends on the emotion and context", value: "contextual-emotions" }
                ]
            },
            {
                question: "How do you approach making friends?",
                type: "multiple",
                options: [
                    { text: "Quickly open up and form many friendships", value: "open-social" },
                    { text: "Slowly build deep, lasting friendships", value: "selective" },
                    { text: "Different levels of friendship for different people", value: "layered" },
                    { text: "Keep most people at arm's length", value: "reserved" }
                ]
            }
        ];

        let currentQuestion = 0;
        let answers = {};
        let timerInterval = null;
        let timeRemaining = 10;

        // --- DOM ELEMENTS ---
        const startBtn = document.getElementById('startBtn');
        const tryAgainBtn = document.getElementById('tryAgainBtn');
        const retakeBtn = document.getElementById('retakeBtn');

        // --- EVENT LISTENERS ---
        startBtn.addEventListener('click', startAssessment);
        tryAgainBtn.addEventListener('click', resetToStart);
        retakeBtn.addEventListener('click', resetToStart);

        function resetToStart() {
            document.getElementById('intro').style.display = 'block';
            document.getElementById('questionnaire').style.display = 'none';
            document.getElementById('timeout').style.display = 'none';
            document.getElementById('results').style.display = 'none';
            document.getElementById('progressFill').style.width = '0%';
            clearInterval(timerInterval); // Stop any lingering timer
        }

        function startAssessment() {
            currentQuestion = 0;
            answers = {};
            document.getElementById('intro').style.display = 'none';
            document.getElementById('questionnaire').style.display = 'block';
            document.getElementById('timeout').style.display = 'none';
            document.getElementById('results').style.display = 'none';
            showQuestion(0);
        }

        function startTimer() {
            timeRemaining = 10;
            clearInterval(timerInterval);
            updateTimerDisplay();

            timerInterval = setInterval(() => {
                timeRemaining--;
                updateTimerDisplay();

                if (timeRemaining <= 0) {
                    clearInterval(timerInterval);
                    handleTimeout();
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const timerFill = document.getElementById('timerFill');
            const timerText = document.getElementById('timerText');
            const timerTextContainer = document.querySelector('.timer-text');

            if (timerFill) {
                timerFill.style.width = (timeRemaining / 10 * 100) + '%';

                // Change color based on time remaining
                if (timeRemaining <= 3) {
                    timerFill.className = 'timer-fill danger';
                    if (timerTextContainer) {
                        timerTextContainer.className = 'timer-text danger';
                    }
                } else if (timeRemaining <= 5) {
                    timerFill.className = 'timer-fill warning';
                    if (timerTextContainer) {
                        timerTextContainer.className = 'timer-text';
                    }
                } else {
                    timerFill.className = 'timer-fill';
                    if (timerTextContainer) {
                        timerTextContainer.className = 'timer-text';
                    }
                }
            }

            if (timerText) {
                timerText.textContent = timeRemaining;
            }
        }

        function handleTimeout() {
            clearInterval(timerInterval);
            document.getElementById('questionnaire').style.display = 'none';
            document.getElementById('timeout').style.display = 'block';
        }

        function showQuestion(index) {
            const questionnaire = document.getElementById('questionnaire');
            const question = questions[index];

            let html = `
                <div class="question-container active">
                    <div class="timer-container">
                        <div class="timer-text">⏱️ Time Remaining: <span id="timerText">10</span> seconds</div>
                        <div class="timer-bar">
                            <div class="timer-fill" id="timerFill"></div>
                        </div>
                    </div>
                    <div class="question">Question ${index + 1} of ${questions.length}: ${question.question}</div>
            `;

            if (question.type === 'multiple') {
                html += '<div class="options">';
                question.options.forEach((option, i) => {
                    html += `
                        <div class="option" onclick="selectOption(${index}, '${option.value}', this)">
                            ${option.text}
                        </div>
                    `;
                });
                html += '</div>';
            } else if (question.type === 'slider') {
                const savedValue = answers[index] || 5;
                html += `
                    <div class="slider-container">
                        <input type="range" class="slider" id="slider${index}"
                                min="${question.min}" max="${question.max}"
                                value="${savedValue}"
                               oninput="updateSlider(${index}, this.value)">
                        <div class="slider-labels">
                            <span>${question.labels[0]}</span>
                            <span>${question.labels[1]}</span>
                        </div>
                    </div>
                `;
                // Auto-save slider value for progression
                answers[index] = savedValue;
            }

            html += `
                <div class="nav-buttons">
                    <button class="nav-btn" onclick="previousQuestion()" 
                             ${index === 0 ? 'disabled' : ''}>Previous</button>
                    <button class="nav-btn" id="nextBtn" onclick="nextQuestion()" 
                             ${question.type === 'multiple' && !answers[index] ? 'disabled' : ''}>
                        ${index === questions.length - 1 ? 'See Results' : 'Next'}
                    </button>
                </div>
            </div>
            `;
            questionnaire.innerHTML = html;
            updateProgress();
            startTimer();
        }

        function selectOption(questionIndex, value, element) {
            answers[questionIndex] = value;

            // Visual feedback
            const options = document.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
            });
            element.classList.add('selected');

            // Enable next button
            const nextBtn = document.getElementById('nextBtn');
            if (nextBtn) {
                nextBtn.disabled = false;
            }
        }

        function updateSlider(questionIndex, value) {
            answers[questionIndex] = parseInt(value);
        }

        function nextQuestion() {
            const question = questions[currentQuestion];
            if (question.type === 'slider') {
                const slider = document.getElementById(`slider${currentQuestion}`);
                if (slider) {
                    answers[currentQuestion] = parseInt(slider.value);
                }
            }

            clearInterval(timerInterval);
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                showQuestion(currentQuestion);
            } else {
                calculateResults();
            }
        }

        function previousQuestion() {
            clearInterval(timerInterval);
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion(currentQuestion);
            }
        }

        function updateProgress() {
            const progress = ((currentQuestion + 1) / questions.length) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        function calculateResults() {
            clearInterval(timerInterval);
            
            const cultures = [
                {
                    name: "Japan",
                    emoji: "🇯🇵",
                    score: 0,
                    color: "#ff6b6b",
                    traits: ["Harmony-focused", "Punctual", "Respectful hierarchy", "Indirect communication", "Group-oriented"],
                    matches: {
                        "harmony": 3, "indirect": 3, "rule-follower": 2, "hierarchical": 2,
                        "controlled": 3, "selective": 2, "private": 2
                    },
                    sliderPreferences: { 2: 8, 6: 3, 10: 7, 12: 3 }
                },
                {
                    name: "Brazil",
                    emoji: "🇧🇷",
                    score: 0,
                    color: "#4ecdc4",
                    traits: ["Warm & expressive", "Flexible time", "Family-oriented", "Physical touch", "Festive"],
                    matches: {
                        "festive": 3, "expressive": 3, "family-first": 2, "flexible-rules": 2,
                        "expressive-emotions": 3, "open-social": 2, "social-dining": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 5, 12: 8 }
                },
                {
                    name: "Germany",
                    emoji: "🇩🇪",
                    score: 0,
                    color: "#95e1d3",
                    traits: ["Punctual", "Direct", "Rule-oriented", "Efficient", "Private"],
                    matches: {
                        "direct": 3, "work-focused": 2, "rule-follower": 3, "direct-comm": 3,
                        "efficient": 3, "private": 2, "meritocratic": 2
                    },
                    sliderPreferences: { 2: 9, 6: 8, 10: 6, 12: 3 }
                },
                {
                    name: "Italy",
                    emoji: "🇮🇹",
                    score: 0,
                    color: "#f38181",
                    traits: ["Family-centered", "Expressive", "Food-focused", "Flexible rules", "Social"],
                    matches: {
                        "family-first": 3, "expressive": 3, "social-dining": 3, "flexible-rules": 2,
                        "expressive-emotions": 2, "festive": 2, "extended": 2
                    },
                    sliderPreferences: { 2: 4, 6: 3, 10: 6, 12: 7 }
                },
                {
                    name: "Sweden",
                    emoji: "🇸🇪",
                    score: 0,
                    color: "#a8e6cf",
                    traits: ["Egalitarian", "Work-life balance", "Environmental", "Consensus-driven", "Reserved"],
                    matches: {
                        "balanced": 3, "egalitarian": 3, "minimal": 2, "controlled": 2,
                        "independent": 2, "reserved": 2, "situational": 2
                    },
                    sliderPreferences: { 2: 7, 6: 7, 10: 3, 12: 2 }
                },
                {
                    name: "India",
                    emoji: "🇮🇳",
                    score: 0,
                    color: "#ffd3b6",
                    traits: ["Family bonds", "Hierarchical", "Spicy food", "Festive", "Spiritual"],
                    matches: {
                        "family-first": 3, "hierarchical": 2, "festive": 2, "extended": 3,
                        "communal": 3, "social-dining": 2, "contextual": 2
                    },
                    sliderPreferences: { 2: 5, 6: 4, 10: 7, 12: 9 }
                },
                {
                    name: "Canada",
                    emoji: "🇨🇦",
                    score: 0,
                    color: "#ffaaa5",
                    traits: ["Polite", "Multicultural", "Nature-loving", "Balanced", "Inclusive"],
                    matches: {
                        "balanced": 2, "diplomatic": 3, "egalitarian": 2, "active": 2,
                        "balanced-family": 2, "layered": 2, "temperate": 2
                    },
                    sliderPreferences: { 2: 6, 6: 6, 10: 4, 12: 4 }
                },
                {
                    name: "Spain",
                    emoji: "🇪🇸",
                    score: 0,
                    color: "#ff8b94",
                    traits: ["Late nights", "Social", "Family-oriented", "Relaxed pace", "Expressive"],
                    matches: {
                        "life-focused": 3, "festive": 2, "social-dining": 3, "expressive": 2,
                        "family-first": 2, "open-social": 2, "flexible-rules": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 5, 12: 6 }
                },
                // African Countries
                {
                    name: "Nigeria",
                    emoji: "🇳🇬",
                    score: 0,
                    color: "#2ecc71",
                    traits: ["Community-focused", "Respectful elders", "Vibrant celebrations", "Entrepreneurial", "Extended family"],
                    matches: {
                        "extended": 3, "hierarchical": 2, "festive": 3, "expressive": 2,
                        "family-first": 3, "communal": 3, "social-dining": 2
                    },
                    sliderPreferences: { 2: 4, 6: 3, 10: 7, 12: 8 }
                },
                {
                    name: "Kenya",
                    emoji: "🇰🇪",
                    score: 0,
                    color: "#e74c3c",
                    traits: ["Hakuna Matata mindset", "Community bonds", "Nature-connected", "Hospitable", "Flexible time"],
                    matches: {
                        "life-focused": 2, "communal": 2, "active": 2, "open-social": 2,
                        "flexible-rules": 2, "extended": 2, "balanced-family": 2
                    },
                    sliderPreferences: { 2: 4, 6: 4, 10: 5, 12: 6 }
                },
                {
                    name: "South Africa",
                    emoji: "🇿🇦",
                    score: 0,
                    color: "#f39c12",
                    traits: ["Ubuntu philosophy", "Diverse", "Direct communication", "Outdoor lifestyle", "Braai culture"],
                    matches: {
                        "direct": 2, "active": 3, "communal": 2, "festive": 2,
                        "balanced": 2, "open-social": 2, "social-dining": 2
                    },
                    sliderPreferences: { 2: 5, 6: 5, 10: 5, 12: 7 }
                },
                {
                    name: "Ghana",
                    emoji: "🇬🇭",
                    score: 0,
                    color: "#9b59b6",
                    traits: ["Respectful", "Joyful", "Traditional values", "Hospitable", "Community-oriented"],
                    matches: {
                        "harmony": 2, "hierarchical": 2, "festive": 2, "extended": 3,
                        "communal": 3, "diplomatic": 2, "family-first": 2
                    },
                    sliderPreferences: { 2: 5, 6: 3, 10: 6, 12: 6 }
                },
                {
                    name: "Ethiopia",
                    emoji: "🇪🇹",
                    score: 0,
                    color: "#1abc9c",
                    traits: ["Ancient traditions", "Coffee ceremony", "Community meals", "Respectful", "Time-flexible"],
                    matches: {
                        "social-dining": 3, "communal": 3, "hierarchical": 2, "extended": 2,
                        "harmony": 2, "flexible-rules": 2, "family-first": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 7, 12: 8 }
                },
                {
                    name: "Morocco",
                    emoji: "🇲🇦",
                    score: 0,
                    color: "#c0392b",
                    traits: ["Hospitable", "Family-honor", "Tea culture", "Negotiation skills", "Traditional"],
                    matches: {
                        "family-first": 3, "hierarchical": 2, "indirect": 2, "social-dining": 2,
                        "extended": 2, "contextual": 2, "mediation": 2
                    },
                    sliderPreferences: { 2: 5, 6: 4, 10: 7, 12: 7 }
                },
                {
                    name: "Tanzania",
                    emoji: "🇹🇿",
                    score: 0,
                    color: "#16a085",
                    traits: ["Pole pole (slowly)", "Respectful", "Community-first", "Nature-connected", "Peaceful"],
                    matches: {
                        "life-focused": 3, "harmony": 2, "communal": 2, "diplomatic": 2,
                        "flexible-rules": 2, "extended": 2, "minimal": 2
                    },
                    sliderPreferences: { 2: 2, 6: 3, 10: 4, 12: 5 }
                },
                {
                    name: "Egypt",
                    emoji: "🇪🇬",
                    score: 0,
                    color: "#d35400",
                    traits: ["Humor-loving", "Family-centered", "Hospitable", "Hierarchical", "Flexible time"],
                    matches: {
                        "family-first": 3, "hierarchical": 2, "expressive": 2, "flexible-rules": 2,
                        "extended": 3, "social-dining": 2, "festive": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 6, 12: 6 }
                },
                {
                    name: "Senegal",
                    emoji: "🇸🇳",
                    score: 0,
                    color: "#27ae60",
                    traits: ["Teranga (hospitality)", "Respectful", "Community solidarity", "Artistic", "Relaxed pace"],
                    matches: {
                        "life-focused": 2, "harmony": 2, "communal": 3, "diplomatic": 2,
                        "extended": 2, "open-social": 2, "flexible-rules": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 5, 12: 5 }
                },
                {
                    name: "Rwanda",
                    emoji: "🇷🇼",
                    score: 0,
                    color: "#2980b9",
                    traits: ["Disciplined", "Community service", "Forward-thinking", "Clean culture", "Unity-focused"],
                    matches: {
                        "rule-follower": 3, "communal": 2, "work-focused": 2, "meritocratic": 2,
                        "harmony": 2, "efficient": 2, "balanced": 2
                    },
                    sliderPreferences: { 2: 7, 6: 6, 10: 6, 12: 4 }
                },
                // Southeast Asian Countries
                {
                    name: "Thailand",
                    emoji: "🇹🇭",
                    score: 0,
                    color: "#ff6f61",
                    traits: ["Sanuk (fun-loving)", "Non-confrontational", "Respectful hierarchy", "Flexible", "Food-centric"],
                    matches: {
                        "harmony": 3, "indirect": 3, "hierarchical": 2, "life-focused": 2,
                        "flexible-rules": 2, "social-dining": 2, "diplomatic": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 5, 12: 9 }
                },
                {
                    name: "Vietnam",
                    emoji: "🇻🇳",
                    score: 0,
                    color: "#ffb347",
                    traits: ["Hardworking", "Family values", "Respectful", "Food culture", "Community-minded"],
                    matches: {
                        "work-focused": 2, "family-first": 3, "hierarchical": 2, "communal": 2,
                        "extended": 2, "social-dining": 2, "indirect": 2
                    },
                    sliderPreferences: { 2: 6, 6: 4, 10: 6, 12: 8 }
                },
                {
                    name: "Indonesia",
                    emoji: "🇮🇩",
                    score: 0,
                    color: "#ff7f50",
                    traits: ["Gotong royong (mutual aid)", "Respectful", "Family-oriented", "Flexible time", "Hospitable"],
                    matches: {
                        "communal": 3, "harmony": 2, "family-first": 2, "hierarchical": 2,
                        "flexible-rules": 2, "extended": 3, "indirect": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 6, 12: 8 }
                },
                {
                    name: "Philippines",
                    emoji: "🇵🇭",
                    score: 0,
                    color: "#4169e1",
                    traits: ["Bayanihan spirit", "Family-first", "Cheerful", "Hospitable", "Flexible"],
                    matches: {
                        "family-first": 3, "extended": 3, "festive": 2, "open-social": 3,
                        "flexible-rules": 2, "expressive-emotions": 2, "communal": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 5, 12: 6 }
                },
                {
                    name: "Singapore",
                    emoji: "🇸🇬",
                    score: 0,
                    color: "#dc143c",
                    traits: ["Kiasu (competitive)", "Efficient", "Multicultural", "Rule-abiding", "Food paradise"],
                    matches: {
                        "work-focused": 3, "rule-follower": 3, "efficient": 3, "meritocratic": 3,
                        "social-dining": 2, "direct": 2, "balanced": 2
                    },
                    sliderPreferences: { 2: 8, 6: 7, 10: 5, 12: 8 }
                },
                {
                    name: "Malaysia",
                    emoji: "🇲🇾",
                    score: 0,
                    color: "#ffd700",
                    traits: ["Multicultural harmony", "Food-obsessed", "Laid-back", "Family values", "Hospitable"],
                    matches: {
                        "harmony": 2, "social-dining": 3, "life-focused": 2, "family-first": 2,
                        "flexible-rules": 2, "communal": 2, "festive": 2
                    },
                    sliderPreferences: { 2: 4, 6: 4, 10: 5, 12: 9 }
                },
                // Caribbean Countries
                {
                    name: "Jamaica",
                    emoji: "🇯🇲",
                    score: 0,
                    color: "#006400",
                    traits: ["Irie vibes", "Music culture", "Laid-back", "Expressive", "Community spirit"],
                    matches: {
                        "life-focused": 3, "expressive": 3, "festive": 3, "flexible-rules": 3,
                        "expressive-emotions": 2, "open-social": 2, "active": 2
                    },
                    sliderPreferences: { 2: 2, 6: 2, 10: 3, 12: 8 }
                },
                {
                    name: "Trinidad & Tobago",
                    emoji: "🇹🇹",
                    score: 0,
                    color: "#ff1744",
                    traits: ["Carnival culture", "Multicultural", "Liming lifestyle", "Musical", "Food fusion"],
                    matches: {
                        "festive": 3, "life-focused": 2, "social-dining": 2, "expressive": 2,
                        "open-social": 3, "flexible-rules": 2, "communal": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 4, 12: 9 }
                },
                {
                    name: "Barbados",
                    emoji: "🇧🇧",
                    score: 0,
                    color: "#1e88e5",
                    traits: ["Polite & formal", "Beach culture", "Cricket passion", "Educational focus", "Rum heritage"],
                    matches: {
                        "diplomatic": 2, "balanced": 2, "rule-follower": 2, "active": 2,
                        "controlled": 2, "meritocratic": 2, "social-dining": 2
                    },
                    sliderPreferences: { 2: 6, 6: 5, 10: 5, 12: 6 }
                },
                {
                    name: "Cuba",
                    emoji: "🇨🇺",
                    score: 0,
                    color: "#d32f2f",
                    traits: ["Resilient", "Music & dance", "Family bonds", "Resourceful", "Warm hospitality"],
                    matches: {
                        "family-first": 3, "festive": 3, "communal": 3, "expressive": 2,
                        "flexible-rules": 2, "extended": 2, "social-dining": 2
                    },
                    sliderPreferences: { 2: 3, 6: 2, 10: 6, 12: 7 }
                },
                {
                    name: "Dominican Republic",
                    emoji: "🇩🇴",
                    score: 0,
                    color: "#0277bd",
                    traits: ["Merengue spirit", "Family-oriented", "Joyful", "Baseball culture", "Flexible time"],
                    matches: {
                        "family-first": 2, "festive": 3, "expressive-emotions": 2, "flexible-rules": 2,
                        "open-social": 2, "extended": 2, "life-focused": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 5, 12: 7 }
                },
                {
                    name: "Haiti",
                    emoji: "🇭🇹",
                    score: 0,
                    color: "#7b1fa2",
                    traits: ["Resilient spirit", "Artistic", "Community solidarity", "Spiritual", "Oral traditions"],
                    matches: {
                        "communal": 3, "extended": 2, "harmony": 2, "contextual": 2,
                        "family-first": 2, "flexible-rules": 2, "layered": 2
                    },
                    sliderPreferences: { 2: 4, 6: 3, 10: 6, 12: 6 }
                },
                {
                    name: "Puerto Rico",
                    emoji: "🇵🇷",
                    score: 0,
                    color: "#f57c00",
                    traits: ["Boricua pride", "Family-centric", "Festive", "Bilingual", "Island time"],
                    matches: {
                        "family-first": 3, "festive": 2, "expressive": 2, "extended": 2,
                        "life-focused": 2, "open-social": 2, "flexible-rules": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 5, 12: 8 }
                },
                {
                    name: "Bahamas",
                    emoji: "🇧🇸",
                    score: 0,
                    color: "#00acc1",
                    traits: ["Island time", "Junkanoo culture", "Friendly", "Beach life", "Relaxed pace"],
                    matches: {
                        "life-focused": 3, "flexible-rules": 2, "open-social": 2, "festive": 2,
                        "balanced": 2, "diplomatic": 2, "active": 2
                    },
                    sliderPreferences: { 2: 2, 6: 3, 10: 4, 12: 5 }
                },
                {
                    name: "Saint Lucia",
                    emoji: "🇱🇨",
                    score: 0,
                    color: "#43a047",
                    traits: ["Creole culture", "Nature-focused", "Relaxed", "Community bonds", "Festival traditions"],
                    matches: {
                        "life-focused": 2, "communal": 2, "harmony": 2, "festive": 2,
                        "flexible-rules": 2, "active": 2, "diplomatic": 2
                    },
                    sliderPreferences: { 2: 3, 6: 3, 10: 4, 12: 6 }
                },
                {
                    name: "Grenada",
                    emoji: "🇬🇩",
                    score: 0,
                    color: "#e53935",
                    traits: ["Spice isle culture", "Friendly", "Carnival spirit", "Family values", "Slow pace"],
                    matches: {
                        "life-focused": 2, "family-first": 2, "festive": 2, "open-social": 2,
                        "flexible-rules": 2, "communal": 2, "harmony": 2
                    },
                    sliderPreferences: { 2: 2, 6: 2, 10: 4, 12: 8 }
                }
            ];

            // Calculate scores for each culture
            cultures.forEach(culture => {
                // Check multiple choice answers
                for (let [key, value] of Object.entries(answers)) {
                    if (typeof value === 'string' && culture.matches[value]) {
                        culture.score += culture.matches[value];
                    }
                }
                // Check slider answers
                for (let [questionIndex, answer] of Object.entries(answers)) {
                    if (typeof answer === 'number') {
                        const preference = culture.sliderPreferences[questionIndex];
                        if (preference !== undefined) {
                            const difference = Math.abs(preference - answer);
                            // Award more points for closer matches on a scale of 1-10
                            culture.score += Math.max(0, 5 - difference); // Less steep drop-off
                        }
                    }
                }
            });

            // Sort by score
            cultures.sort((a, b) => b.score - a.score);

            // Calculate percentages
            const maxScore = cultures[0].score > 0 ? cultures[0].score : 1;
            cultures.forEach(culture => {
                culture.percentage = Math.round((culture.score / maxScore) * 100);
            });

            displayResults(cultures);
        }

        function displayResults(cultures) {
            document.getElementById('questionnaire').style.display = 'none';
            document.getElementById('timeout').style.display = 'none';
            document.getElementById('results').style.display = 'block';
            const resultsList = document.getElementById('resultsList');
            let html = '';
            
            // Show top 5 matches
            cultures.slice(0, 5).forEach((culture, index) => {
                if (culture.percentage > 0) { // Only show cultures with a score
                     html += `
                        <div class="result-card" style="border-color: ${culture.color}; animation-delay: ${index * 0.1}s">
                            <div class="country-name">${culture.emoji} ${culture.name}</div>
                            <div class="match-percentage">${culture.percentage}% Match</div>
                            <div class="cultural-traits">
                                <strong>Cultural Strengths:</strong><br>
                                ${culture.traits.map(trait => `<span class="trait">${trait}</span>`).join('')}
                            </div>
                        </div>
                    `;
                }
            });

            if (html === '') {
                html = '<p>Your answers didn\'t strongly match any specific culture profile. Try taking the assessment again!</p>';
            }

            resultsList.innerHTML = html;
        }

    </script>
</body>
</html>
