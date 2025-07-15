<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบแปลภาษา (ไทย ↔ เกาหลี) ด้วยเสียง (Gemini AI)</title>
    <link rel="icon" href="https://makubtrader.com/ccdc/Favicon.png" type="image/png" sizes="16x16">
    <link rel="icon" href="https://makubtrader.com/ccdc/Favicon.png" type="image/png" sizes="32x32">
    <link rel="apple-touch-icon" href="https://makubtrader.com/ccdc/Favicon.png">
    <link rel="shortcut icon" href="https://makubtrader.com/ccdc/Favicon.png">
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        /* General Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Sarabun', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Changed to flex-start for top alignment on larger screens */
            padding: 20px;
            color: #333;
            overflow-y: auto; /* Allow scrolling if content is long */
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px; /* More rounded corners */
            padding: 30px 20px; /* Adjusted padding for mobile */
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15); /* Deeper shadow */
            max-width: 600px; /* Max width for mobile/tablet */
            width: 100%;
            backdrop-filter: blur(10px);
            margin-top: 20px; /* Top margin */
            margin-bottom: 20px; /* Bottom margin */
        }

        @media (min-width: 768px) {
            .container {
                padding: 40px; /* More padding on larger screens */
                max-width: 800px; /* Wider on larger screens */
                margin-top: 50px;
                margin-bottom: 50px;
            }
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 25px; /* Adjusted margin */
            font-size: 2.2em; /* Adjusted size for mobile */
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: 600;
            letter-spacing: -0.5px; /* Slightly reduced letter spacing */
        }

        @media (min-width: 768px) {
            h1 {
                font-size: 2.8em;
            }
        }

        /* Language Switcher Navigation */
        .language-switcher {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 30px; /* Space below switcher */
            flex-wrap: wrap; /* Allow wrapping on small screens */
            padding: 10px 0;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05); /* Subtle separator */
        }

        .nav-btn {
            padding: 10px 15px;
            border-radius: 8px;
            text-decoration: none;
            color: #555;
            background: #e2e8f0;
            font-weight: 600;
            font-size: 0.95em;
            transition: all 0.3s ease;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.08);
            display: flex;
            align-items: center;
            justify-content: center;
            min-width: 80px; /* Ensure buttons have a minimum width */
            text-align: center;
        }

        .nav-btn:hover {
            transform: translateY(-1px);
            box-shadow: 0 5px 12px rgba(0, 0, 0, 0.12);
            background: #dce3ec;
        }

        /* Active button style */
        .nav-btn.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.25);
            cursor: default; /* Not clickable if active */
            transform: none; /* No hover effect on active */
            pointer-events: none; /* Disable clicks on active */
        }

        .section {
            margin-bottom: 25px; /* Reduced margin between sections */
            padding: 20px; /* Adjusted padding */
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border: none; /* Removed border for cleaner look */
        }

        .section h2 {
            color: #4a4a4a; /* Darker grey for headings */
            margin-bottom: 15px; /* Adjusted margin */
            font-size: 1.4em; /* Adjusted heading size */
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 600; /* Bolder */
            text-align: center; /* Centered heading */
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05); /* Subtle bottom border */
            justify-content: center; /* Center content horizontally */
        }

        .section h3 {
            font-size: 1.1em;
            margin-top: 15px;
            margin-bottom: 10px;
            color: #555;
        }

        .icon {
            font-size: 1.1em;
            color: #764ba2;
            margin-right: 5px; /* Added space from text */
        }

        /* API Key Section */
        .api-setup {
            margin-bottom: 30px;
            padding: 20px; /* Adjusted padding */
            background: linear-gradient(135deg, #f8f9ff 0%, #e8f2ff 100%);
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border: 2px solid #a8b0e7; /* Lighter border color */
            position: relative;
            overflow: hidden;
        }

        .api-setup::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px; /* Thinner top line */
            background: linear-gradient(45deg, #667eea, #764ba2);
        }

        .api-setup .warning {
            background: #fff3cd;
            border-left: 5px solid #ffc107;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
            font-size: 0.95em;
            color: #856404;
            line-height: 1.6;
        }

        .api-setup .warning a {
            color: #667eea;
            font-weight: bold;
            text-decoration: none;
            border-bottom: 1px dotted #667eea;
        }

        .api-setup .warning a:hover {
            text-decoration: underline;
            color: #5a67d8;
        }

        .api-input-group {
            display: flex;
            flex-direction: column; /* Stack input and button vertically on mobile */
            gap: 15px; /* Increased gap */
            margin-bottom: 15px;
            flex-wrap: wrap; /* Retain for wider screens if needed */
        }

        .api-input {
            width: 100%; /* Full width */
            padding: 12px; /* Adjusted padding */
            border: 2px solid #e2e8f0;
            border-radius: 8px; /* More rounded */
            font-size: 0.95em; /* Adjusted font size */
            background: white;
            transition: all 0.3s ease;
            font-family: 'Courier New', monospace;
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.06); /* Inner shadow for depth */
        }

        .api-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.2); /* More prominent focus shadow */
        }

        .api-input::placeholder {
            color: #a0aec0;
            font-style: italic;
        }

        .api-btn {
            width: 100%; /* Full width on mobile */
            padding: 12px 20px; /* Adjusted padding */
            border: none;
            border-radius: 8px; /* More rounded */
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.95em; /* Adjusted font size */
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            box-shadow: 0 3px 10px rgba(102, 126, 234, 0.2); /* Adjusted shadow */
        }

        .api-btn:hover {
            transform: translateY(-1px); /* Reduced hover lift */
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }

        .api-btn.remove {
            background: linear-gradient(45deg, #ff6b6b, #ee5a6f);
            box-shadow: 0 3px 10px rgba(255, 107, 107, 0.2);
        }

        .api-btn.remove:hover {
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.3);
        }

        .api-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .api-status {
            margin-top: 15px;
            padding: 10px 15px; /* Adjusted padding */
            border-radius: 8px;
            font-size: 0.9em; /* Smaller font size */
            font-weight: 600;
            text-align: center;
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px; /* Smaller gap */
            cursor: pointer;
        }

        .api-status::before {
            content: '✅';
            font-size: 1.1em; /* Slightly smaller icon */
        }

        /* Mode Selector */
        .mode-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            justify-content: center;
            flex-wrap: wrap; /* Allow wrapping on small screens */
        }

        .mode-selector .btn {
            flex-grow: 1;
            min-width: 120px; /* Ensure buttons are not too small */
            padding: 12px 15px;
            font-size: 0.9em;
            background: #e2e8f0; /* Default background for inactive buttons */
            color: #555;
            box-shadow: none;
            border: 1px solid #cbd5e0;
        }

        .mode-selector .btn.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.2);
            border: none;
        }
        .mode-selector .btn:hover:not(.active) {
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            background: #dce3ec;
        }


        /* Voice Controls */
        .voice-controls {
            display: flex;
            flex-direction: column; /* Stack buttons vertically on mobile */
            gap: 10px; /* Reduced gap */
            margin-bottom: 15px;
            justify-content: center;
        }

        @media (min-width: 480px) { /* Breakpoint for slightly larger mobile screens */
            .voice-controls {
                flex-direction: row; /* Buttons side-by-side */
                flex-wrap: wrap; /* Allow wrapping */
            }
            .btn {
                flex-grow: 1; /* Distribute space evenly */
                min-width: unset; /* Remove minimum width */
                width: auto;
            }
        }

        .btn {
            width: 100%; /* Full width on mobile */
            padding: 12px 20px; /* Adjusted padding */
            border: none;
            border-radius: 8px; /* More rounded */
            font-size: 0.95em; /* Adjusted font size */
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            justify-content: center; /* Center content in button */
            gap: 8px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1); /* Adjusted shadow */
        }

        .btn:hover {
            transform: translateY(-1px); /* Reduced hover lift */
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
        }

        .btn-primary {
            background: linear-gradient(45deg, #5a67d8, #6d4ed9); /* Adjusted shade */
            color: white;
        }

        .btn-danger {
            background: linear-gradient(45deg, #ef4444, #dc2626); /* Adjusted shade */
            color: white;
        }

        .btn-success {
            background: linear-gradient(45deg, #10b981, #059669); /* Adjusted shade */
            color: white;
        }

        .btn-info {
            background: linear-gradient(45deg, #3b82f6, #2563eb); /* Adjusted shade */
            color: white;
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .recording {
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0%, 40%, 100% { transform: scale(1); box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1); } /* Adjusted shadow */
            50% { transform: scale(1.02); box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15); } /* Adjusted scale and shadow */
            100% { transform: scale(1); box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1); }
        }

        textarea {
            width: 100%;
            min-height: 100px; /* Reduced initial height on mobile */
            padding: 12px; /* Adjusted padding */
            border: 2px solid #e0e0e0;
            border-radius: 8px; /* More rounded */
            font-size: 1em;
            font-family: inherit;
            resize: vertical;
            transition: border-color 0.3s ease, background 0.3s ease;
            background: #fdfdfd; /* Lighter background */
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.06); /* Inner shadow */
        }

        textarea:focus {
            outline: none;
            border-color: #667eea;
            background: white;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.2);
        }

        .status {
            margin-top: 10px; /* Reduced margin */
            padding: 10px; /* Adjusted padding */
            border-radius: 6px; /* Slightly less rounded */
            font-weight: 500;
            text-align: center;
            transition: all 0.3s ease;
            font-size: 0.85em; /* Smaller font size */
        }

        .status.listening {
            background: #e3f2fd;
            color: #1976d2;
            border: 1px solid #90caf9;
        }

        .status.processing {
            background: #fff3e0;
            color: #f57c00;
            border: 1px solid #ffcc02;
        }

        .status.error {
            background: #ffebee;
            color: #d32f2f;
            border: 1px solid #ffcdd2;
        }

        .status.success {
            background: #e8f5e8;
            color: #2e7d32;
            border: 1px solid #c8e6c9;
        }

        .status.info {
            background: #e3f2fd;
            color: #1976d2;
            border: 1px solid #90caf9;
        }

        .translate-btn {
            width: 100%;
            margin-top: 10px; /* Reduced margin */
            padding: 12px; /* Adjusted padding */
            font-size: 1em; /* Adjusted font size */
        }

        .section.result-section {
            background: linear-gradient(135deg, #eef2f7 0%, #e0e6f0 100%); /* Lighter background for result section */
        }

        .wave-animation {
            display: inline-block;
            width: 20px;
            height: 20px;
            background: currentColor;
            border-radius: 50%;
            animation: wave 1.4s ease-in-out infinite both;
        }

        @keyframes wave {
            0%, 40%, 100% { transform: scaleY(0.4); }
            20% { transform: scaleY(1.0); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎤 ระบบแปลภาษา (ไทย ↔ ญี่ปุ่น)</h1>
        
        <div class="language-switcher">
            <a href="https://nessakura.github.io/thai-english-voice-translator/" class="nav-btn" id="navEnglish">🇹🇭-🇬🇧</a>
            <a href="https://nessakura.github.io/thai-japan-voice-translator/" class="nav-btn" id="navJapanese">🇹🇭-🇯🇵</a>
            <a href="https://nessakura.github.io/thai-korea-voice-translator/" class="nav-btn" id="navKorean">🇹🇭-🇰🇷</a>
            <a href="https://nessakura.github.io/thai-china-voice-translator/" class="nav-btn" id="navChinese">🇹🇭-🇨🇳</a>
        </div>

        <div class="api-setup" id="apiSetupSection">
            <h2><span class="icon">🔑</span> ตั้งค่า Gemini API Key</h2>
            <div class="warning">
                ⚠️ <strong>คำเตือนด้านความปลอดภัย:</strong> API Key ของคุณจะถูกเก็บในเบราว์เซอร์เท่านั้น และจะถูกล้างหากคุณล้างข้อมูลการเข้าชมเว็บไซต์<br>
                📝 หากยังไม่มี API Key สามารถสร้างได้ฟรีที่ 
                <a href="https://aistudio.google.com/app/apikey" target="_blank">Google AI Studio</a><br>
                💡 <strong>วิธีใช้:</strong> ใส่ API Key → กดบันทึก → เริ่มใช้งานได้เลย!
            </div>
            
            <div class="api-input-group">
                <input 
                    type="password" 
                    id="apiKeyInput" 
                    class="api-input" 
                    placeholder="ใส่ Gemini API Key ของคุณที่นี่... (เช่น: AIzaSyC...)" 
                    autocomplete="off"
                >
                <button class="api-btn" id="saveApiKeyBtn">
                    💾 บันทึก API Key
                </button>
            </div>
            
            <button class="api-btn remove" id="removeApiKeyBtn" style="display: none;">
                🗑️ ลบ API Key
            </button>
        </div>

        <div id="apiKeyStatusDisplay" class="api-status" style="display: none;">
            API Key ถูกตั้งค่าเรียบร้อยแล้ว! คลิกเพื่อแก้ไข.
        </div>

        <div class="mode-selector">
            <button class="btn btn-primary active" id="modeThaiToJapaneseBtn">
                🇹🇭 ➡️ 🇯🇵
            </button>
            <button class="btn btn-primary" id="modeJapaneseToThaiBtn">
                🇯🇵 ➡️ 🇹🇭
            </button>
        </div>

        <div class="section" id="thaiToJapaneseSection">
            <h2><span class="icon">🇹🇭➡️🇯🇵</span> ไทย ➡️ ญี่ปุ่น</h2>
            <div class="voice-controls">
                <button class="btn btn-primary" id="startThaiBtn" disabled>
                    <span>🎤</span> เริ่มพูด (ไทย)
                </button>
                <button class="btn btn-danger" id="stopThaiBtn" disabled>
                    <span>⏹️</span> หยุดบันทึก
                </button>
                <button class="btn btn-success" id="clearAllBtn">
                    <span>🗑️</span> ล้างข้อมูลทั้งหมด
                </button>
            </div>
            <div class="status" id="status">กรุณาใส่ Gemini API Key ก่อนใช้งาน</div>
            
            <h3>ข้อความภาษาไทย:</h3>
            <textarea id="thaiText" placeholder="พูดหรือพิมพ์ข้อความภาษาไทย..."></textarea>
            <button class="btn btn-primary translate-btn" id="translateThaiToJapaneseBtn" disabled>
                <span>🔄</span> แปลเป็นภาษาญี่ปุ่น
            </button>
            
            <h3 style="margin-top: 20px;">ผลการแปล (ภาษาญี่ปุ่น):</h3>
            <textarea id="japaneseText" placeholder="ผลการแปลจะแสดงที่นี่..." readonly></textarea>
            <button class="btn btn-info translate-btn" id="listenJapaneseBtn" disabled>
                <span>🔊</span> อ่านออกเสียง (ญี่ปุ่น)
            </button>
        </div>

        <div class="section result-section" id="japaneseToThaiSection" style="display: none;">
            <h2><span class="icon">🇯🇵➡️🇹🇭</span> ญี่ปุ่น ➡️ ไทย</h2>
            <div class="voice-controls">
                <button class="btn btn-info" id="startJapaneseBtn" disabled>
                    <span>🎙️</span> เริ่มพูด (ญี่ปุ่น)
                </button>
                <button class="btn btn-danger" id="stopJapaneseBtn" disabled>
                    <span>⏹️</span> หยุดบันทึก
                </button>
            </div>
            
            <h3>ข้อความภาษาญี่ปุ่น:</h3>
            <textarea id="japaneseListenText" placeholder="พูดหรือพิมพ์ข้อความภาษาญี่ปุ่น..."></textarea>
            <button class="btn btn-primary translate-btn" id="translateJapaneseToThaiBtn" disabled>
                <span>🔄</span> แปลเป็นภาษาไทย
            </button>
            
            <h3 style="margin-top: 20px;">ผลการแปล (ภาษาไทย):</h3>
            <textarea id="thaiTranslatedText" placeholder="ผลการแปลจะแสดงที่นี่..." readonly></textarea>
            <button class="btn btn-success translate-btn" id="listenThaiBtn" disabled>
                <span>🔊</span> อ่านออกเสียง (ไทย)
            </button>
        </div>
    </div>

    <script>
        class BiDirectionalVoiceTranslator {
            constructor() {
                this.geminiApiKey = localStorage.getItem('geminiApiKey') || '';
                this.speechSynthesisUtteranceJapanese = null;
                this.speechSynthesisUtteranceThai = null;
                this.currentMode = 'thaiToJapanese'; // Default mode: Thai to Japanese

                this.initializeElements();
                this.setupGlobalEventListeners();
                this.setupThaiToJapaneseMode();
                this.setupJapaneseToThaiMode();
                this.checkApiKeyStatus();
                this.switchMode(this.currentMode); // Set initial display mode
                this.highlightActiveNavButton(); // Highlight the current page's button
            }

            initializeElements() {
                this.apiSetupSection = document.getElementById('apiSetupSection');
                this.apiKeyInput = document.getElementById('apiKeyInput');
                this.saveApiKeyBtn = document.getElementById('saveApiKeyBtn');
                this.removeApiKeyBtn = document.getElementById('removeApiKeyBtn');
                this.apiKeyStatusDisplay = document.getElementById('apiKeyStatusDisplay');
                this.statusDiv = document.getElementById('status');
                this.clearAllBtn = document.getElementById('clearAllBtn');

                // Mode selector buttons
                this.modeThaiToJapaneseBtn = document.getElementById('modeThaiToJapaneseBtn');
                this.modeJapaneseToThaiBtn = document.getElementById('modeJapaneseToThaiBtn');
                this.thaiToJapaneseSection = document.getElementById('thaiToJapaneseSection');
                this.japaneseToThaiSection = document.getElementById('japaneseToThaiSection');


                // Thai to Japanese elements
                this.startThaiBtn = document.getElementById('startThaiBtn');
                this.stopThaiBtn = document.getElementById('stopThaiBtn');
                this.thaiText = document.getElementById('thaiText');
                this.translateThaiToJapaneseBtn = document.getElementById('translateThaiToJapaneseBtn');
                this.japaneseText = document.getElementById('japaneseText');
                this.listenJapaneseBtn = document.getElementById('listenJapaneseBtn');

                // Japanese to Thai elements
                this.startJapaneseBtn = document.getElementById('startJapaneseBtn');
                this.stopJapaneseBtn = document.getElementById('stopJapaneseBtn');
                this.japaneseListenText = document.getElementById('japaneseListenText');
                this.translateJapaneseToThaiBtn = document.getElementById('translateJapaneseToThaiBtn');
                this.thaiTranslatedText = document.getElementById('thaiTranslatedText');
                this.listenThaiBtn = document.getElementById('listenThaiBtn');
            }

            setupGlobalEventListeners() {
                this.saveApiKeyBtn.addEventListener('click', () => this.saveApiKey());
                this.removeApiKeyBtn.addEventListener('click', () => this.removeApiKey());
                this.apiKeyInput.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') this.saveApiKey();
                });
                this.apiKeyStatusDisplay.addEventListener('click', () => {
                    this.apiSetupSection.style.display = 'block';
                    this.apiKeyStatusDisplay.style.display = 'none';
                    this.apiKeyInput.value = this.geminiApiKey;
                    this.apiKeyInput.disabled = false;
                    this.saveApiKeyBtn.style.display = 'inline-block';
                    this.removeApiKeyBtn.style.display = 'inline-block';
                    this.apiKeyInput.focus();
                    this.updateStatus('คุณกำลังแก้ไข API Key', 'info');
                    this.disableAllFeatures();
                });
                this.clearAllBtn.addEventListener('click', () => this.clearAll());
                
                // Mode selector event listeners
                this.modeThaiToJapaneseBtn.addEventListener('click', () => this.switchMode('thaiToJapanese'));
                this.modeJapaneseToThaiBtn.addEventListener('click', () => this.switchMode('japaneseToThai'));
            }

            highlightActiveNavButton() {
                const navButtons = document.querySelectorAll('.language-switcher .nav-btn');
                navButtons.forEach(button => {
                    if (button.href === window.location.href) {
                        button.classList.add('active');
                    }
                });
            }

            switchMode(mode) {
                this.currentMode = mode;
                this.stopAllAudioAndRecognition();
                this.clearAllTextareas(); // Clear textareas when switching mode

                if (mode === 'thaiToJapanese') {
                    this.thaiToJapaneseSection.style.display = 'block';
                    this.japaneseToThaiSection.style.display = 'none';
                    this.modeThaiToJapaneseBtn.classList.add('active');
                    this.modeJapaneseToThaiBtn.classList.remove('active');
                    this.updateStatus('พร้อมใช้งาน: ไทย ➡️ ญี่ปุ่น', 'success');
                } else { // japaneseToThai
                    this.thaiToJapaneseSection.style.display = 'none';
                    this.japaneseToThaiSection.style.display = 'block';
                    this.modeThaiToJapaneseBtn.classList.remove('active');
                    this.modeJapaneseToThaiBtn.classList.add('active');
                    this.updateStatus('พร้อมใช้งาน: ญี่ปุ่น ➡️ ไทย', 'success');
                }
                this.checkApiKeyStatus(); // Re-check and enable features based on API key
            }

            enableAllFeatures() {
                this.startThaiBtn.disabled = false;
                this.startJapaneseBtn.disabled = false;
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            disableAllFeatures() {
                this.startThaiBtn.disabled = true;
                this.stopThaiBtn.disabled = true;
                this.translateThaiToJapaneseBtn.disabled = true;
                this.listenJapaneseBtn.disabled = true;

                this.startJapaneseBtn.disabled = true;
                this.stopJapaneseBtn.disabled = true;
                this.translateJapaneseToThaiBtn.disabled = true;
                this.listenThaiBtn.disabled = true;
            }

            saveApiKey() {
                const inputKey = this.apiKeyInput.value.trim();
                if (!inputKey) {
                    alert('กรุณาใส่ Gemini API Key ก่อนบันทึก');
                    return;
                }
                if (inputKey.length < 20 || !inputKey.startsWith('AIza')) {
                    alert('API Key ดูเหมือนจะไม่ถูกต้อง กรุณาตรวจสอบอีกครั้ง (เช่น: AIzaSyC...)');
                    return;
                }

                this.geminiApiKey = inputKey;
                localStorage.setItem('geminiApiKey', this.geminiApiKey);
                this.checkApiKeyStatus();
                this.updateStatus(`บันทึก API Key เรียบร้อย! พร้อมใช้งาน: ${this.currentMode === 'thaiToJapanese' ? 'ไทย ➡️ ญี่ปุ่น' : 'ญี่ปุ่น ➡️ ไทย'}`, 'success');
            }

            removeApiKey() {
                if (confirm('คุณแน่ใจหรือไม่ว่าต้องการลบ API Key?')) {
                    localStorage.removeItem('geminiApiKey');
                    this.geminiApiKey = '';
                    this.checkApiKeyStatus();
                    this.clearAll();
                    this.updateStatus('ลบ API Key เรียบร้อย กรุณาใส่ API Key ใหม่', 'info');
                }
            }

            updateStatus(message, type) {
                this.statusDiv.innerHTML = message;
                this.statusDiv.className = 'status';
                if (type) {
                    this.statusDiv.classList.add(type);
                }
            }

            updateTranslateButtonStates() {
                this.translateThaiToJapaneseBtn.disabled = !this.thaiText.value.trim() || !this.geminiApiKey;
                this.translateJapaneseToThaiBtn.disabled = !this.japaneseListenText.value.trim() || !this.geminiApiKey;
            }

            updateListenButtonStates() {
                this.listenJapaneseBtn.disabled = !this.japaneseText.value.trim();
                this.listenThaiBtn.disabled = !this.thaiTranslatedText.value.trim();
            }

            clearAll() {
                this.clearAllTextareas();
                if(this.geminiApiKey) {
                    this.updateStatus('ล้างข้อมูลเรียบร้อย', 'success');
                } else {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
                this.stopAllAudioAndRecognition();
            }

            clearAllTextareas() {
                this.thaiText.value = '';
                this.japaneseText.value = '';
                this.japaneseListenText.value = '';
                this.thaiTranslatedText.value = '';
            }

            stopAllAudioAndRecognition() {
                if (this.isRecordingThai) this.stopRecordingThai();
                if (this.isRecordingJapanese) this.stopRecordingJapanese();
                if (window.speechSynthesis.speaking) window.speechSynthesis.cancel();
            }

            async translateText(sourceText, sourceLang, targetLang) {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return '';
                }
                if (!sourceText.trim()) {
                    this.updateStatus(`กรุณากรอกข้อความ ${sourceLang} ที่ต้องการแปล`, 'error');
                    return '';
                }

                const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${this.geminiApiKey}`;
                
                const prompt = `Translate the following ${sourceLang} text to ${targetLang}. Respond only with the ${targetLang} translation, without any additional comments, prefixes, or explanations, and avoid markdown if possible.
                
                ${sourceLang}: "${sourceText}"
                
                ${targetLang}:`;

                try {
                    const response = await fetch(API_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            contents: [{ parts: [{ text: prompt }] }],
                            generationConfig: { 
                                temperature: 0.2,
                                maxOutputTokens: 200
                            }
                        })
                    });

                    if (!response.ok) {
                        const errorData = await response.json();
                        if (errorData.error && errorData.error.status === 'RESOURCE_EXHAUSTED') {
                             throw new Error('โควต้าการใช้งาน API หมด กรุณาลองใหม่ภายหลัง');
                        }
                        throw new Error(errorData.error.message || `HTTP error! status: ${response.status}`);
                    }

                    const data = await response.json();
                    
                    if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts[0]) {
                        let translated = data.candidates[0].content.parts[0].text.trim();
                        // Clean up potential prefixes from Gemini
                        if (translated.toLowerCase().startsWith(`${targetLang.toLowerCase()}:`)) {
                            translated = translated.substring(`${targetLang.toLowerCase()}:`.length).trim();
                        }
                        return translated;
                    } else {
                        if (data.promptFeedback && data.promptFeedback.blockReason) {
                            throw new Error(`คำร้องขอถูกบล็อก: ${data.promptFeedback.blockReason}. อาจเป็นเพราะเนื้อหาไม่เหมาะสม.`);
                        }
                        throw new Error('ไม่ได้รับการตอบสนองที่คาดหวังจาก Gemini API หรือผลลัพธ์ว่างเปล่า');
                    }
                } catch (error) {
                    console.error('Translation error with Gemini:', error);
                    let errorMessage = 'ไม่สามารถแปลภาษาได้';
                    if (error.message.includes('API key not valid')) {
                        errorMessage = 'API Key ไม่ถูกต้อง กรุณาตรวจสอบและใส่ใหม่';
                    } else if (error.message.includes('Quota') || error.message.includes('โควต้า')) {
                        errorMessage = 'โควต้าการใช้งาน API หมด กรุณาลองใหม่ภายหลัง';
                    } else if (error.message.includes('blocked')) {
                        errorMessage = `เกิดข้อผิดพลาด: ${error.message}`;
                    } else {
                        errorMessage = `เกิดข้อผิดพลาด: ${error.message}`;
                    }
                    this.updateStatus(errorMessage, 'error');
                    return `Error: ${errorMessage}`;
                }
            }

            handleRecognitionError(event, lang) {
                let errorMessage = `เกิดข้อผิดพลาดในการรู้จำเสียง (${lang})`;
                if (event.error === 'no-speech') {
                    errorMessage = `ไม่พบเสียงพูด (${lang})`;
                } else if (event.error === 'not-allowed') {
                    errorMessage = `ไม่ได้รับอนุญาตให้ใช้ไมโครโฟน กรุณาอนุญาตในเบราว์เซอร์ (${lang})`;
                } else if (event.error === 'aborted') {
                    errorMessage = `การบันทึกเสียงถูกยกเลิก (${lang})`;
                }
                this.updateStatus(errorMessage, 'error');
            }

            // --- Thai to Japanese Mode ---
            setupThaiToJapaneseMode() {
                this.isRecordingThai = false;
                if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
                    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                    this.recognitionThai = new SpeechRecognition();
                    this.recognitionThai.continuous = true;
                    this.recognitionThai.interimResults = true;
                    this.recognitionThai.lang = 'th-TH';

                    this.recognitionThai.onstart = () => this.onThaiRecognitionStart();
                    this.recognitionThai.onresult = (event) => this.onThaiRecognitionResult(event);
                    this.recognitionThai.onerror = (event) => this.handleRecognitionError(event, 'ไทย');
                    this.recognitionThai.onend = () => this.onThaiRecognitionEnd();
                } else {
                    this.startThaiBtn.disabled = true;
                    this.updateStatus('เบราว์เซอร์ไม่รองรับการรู้จำเสียงภาษาไทย', 'error');
                }

                this.startThaiBtn.addEventListener('click', () => this.startRecordingThai());
                this.stopThaiBtn.addEventListener('click', () => this.stopRecordingThai());
                this.translateThaiToJapaneseBtn.addEventListener('click', () => this.translateThaiToJapanese());
                this.listenJapaneseBtn.addEventListener('click', () => this.speakJapaneseText());
                this.thaiText.addEventListener('input', () => this.updateTranslateButtonStates());
                this.japaneseText.addEventListener('input', () => this.updateListenButtonStates());
            }

            startRecordingThai() {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return;
                }
                if (this.isRecordingJapanese) { this.stopRecordingJapanese(); }
                if (this.recognitionThai && !this.isRecordingThai) {
                    this.recognitionThai.start();
                }
            }

            stopRecordingThai() {
                if (this.recognitionThai && this.isRecordingThai) {
                    this.recognitionThai.stop();
                }
                this.isRecordingThai = false;
                this.startThaiBtn.disabled = !this.geminiApiKey;
                this.stopThaiBtn.disabled = true;
                this.startThaiBtn.classList.remove('recording');
            }

            onThaiRecognitionStart() {
                this.isRecordingThai = true;
                this.updateStatus('กำลังฟัง (ไทย)... <span class="wave-animation"></span>', 'listening');
                this.startThaiBtn.disabled = true;
                this.stopThaiBtn.disabled = false;
                this.startThaiBtn.classList.add('recording');
                this.thaiText.value = '';
                this.japaneseText.value = '';
                this.updateListenButtonStates();
            }

            onThaiRecognitionResult(event) {
                let finalTranscript = '';
                let interimTranscript = '';
                for (let i = event.resultIndex; i < event.results.length; i++) {
                    const transcript = event.results[i][0].transcript;
                    if (event.results[i].isFinal) {
                        finalTranscript += transcript;
                    } else {
                        interimTranscript += transcript;
                    }
                }
                this.thaiText.value = finalTranscript + interimTranscript;
                if (finalTranscript) {
                    this.updateStatus('พบข้อความไทยแล้ว กำลังรอให้คุณพูดจบ...', 'success');
                }
                this.updateTranslateButtonStates();
            }

            onThaiRecognitionEnd() {
                this.stopRecordingThai();
                if (this.thaiText.value.trim()) {
                    this.updateStatus('บันทึกเสียงไทยเสร็จสิ้น กำลังแปลภาษา...', 'processing');
                    this.translateThaiToJapanese();
                } else {
                    this.updateStatus('กดปุ่ม "เริ่มพูด (ไทย)" เพื่อเริ่มต้น', 'info');
                }
            }

            async translateThaiToJapanese() {
                this.updateStatus('กำลังแปลภาษาไทยเป็นญี่ปุ่น...', 'processing');
                this.translateThaiToJapaneseBtn.disabled = true;
                this.japaneseText.value = 'Translating...';
                this.listenJapaneseBtn.disabled = true;

                const result = await this.translateText(this.thaiText.value, 'Thai', 'Japanese');
                this.japaneseText.value = result;

                if (result && !result.startsWith('Error:')) {
                    this.updateStatus('แปลภาษาไทยเป็นญี่ปุ่นเสร็จสิ้น', 'success');
                    this.speakJapaneseText();
                } else if (result.startsWith('Error:')) {
                    this.japaneseText.value = result;
                } else {
                    this.updateStatus('ไม่มีข้อความให้แปล หรือเกิดข้อผิดพลาด', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            speakJapaneseText() {
                const text = this.japaneseText.value.trim();
                if (!text || text.startsWith('Error:')) {
                    this.updateStatus('ไม่มีข้อความภาษาญี่ปุ่นให้อ่าน', 'info');
                    return;
                }

                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel();
                }

                this.speechSynthesisUtteranceJapanese = new SpeechSynthesisUtterance(text);
                this.speechSynthesisUtteranceJapanese.lang = 'ja-JP'; // Japanese (Japan)
                
                this.speechSynthesisUtteranceJapanese.onerror = (event) => {
                    console.error('Speech synthesis error (Japanese):', event.error);
                    this.updateStatus(`ไม่สามารถอ่านออกเสียงภาษาญี่ปุ่นได้: ${event.error}`, 'error');
                };
                this.speechSynthesisUtteranceJapanese.onstart = () => {
                    this.updateStatus('กำลังอ่านออกเสียง (ญี่ปุ่น)...', 'processing');
                    this.listenJapaneseBtn.disabled = true;
                };
                this.speechSynthesisUtteranceJapanese.onend = () => {
                    this.updateStatus('อ่านออกเสียง (ญี่ปุ่น) เสร็จสิ้น', 'success');
                    this.listenJapaneseBtn.disabled = false;
                };

                window.speechSynthesis.speak(this.speechSynthesisUtteranceJapanese);
            }

            // --- Japanese to Thai Mode ---
            setupJapaneseToThaiMode() {
                this.isRecordingJapanese = false;
                if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
                    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                    this.recognitionJapanese = new SpeechRecognition();
                    this.recognitionJapanese.continuous = true;
                    this.recognitionJapanese.interimResults = true;
                    this.recognitionJapanese.lang = 'ja-JP'; // Japanese (Japan)

                    this.recognitionJapanese.onstart = () => this.onJapaneseRecognitionStart();
                    this.recognitionJapanese.onresult = (event) => this.onJapaneseRecognitionResult(event);
                    this.recognitionJapanese.onerror = (event) => this.handleRecognitionError(event, 'ญี่ปุ่น');
                    this.recognitionJapanese.onend = () => this.onJapaneseRecognitionEnd();
                } else {
                    this.startJapaneseBtn.disabled = true;
                    this.updateStatus('เบราว์เซอร์ไม่รองรับการรู้จำเสียงภาษาญี่ปุ่น', 'error');
                }

                this.startJapaneseBtn.addEventListener('click', () => this.startRecordingJapanese());
                this.stopJapaneseBtn.addEventListener('click', () => this.stopRecordingJapanese());
                this.japaneseListenText.addEventListener('input', () => this.updateTranslateButtonStates());
                this.thaiTranslatedText.addEventListener('input', () => this.updateListenButtonStates());
                this.translateJapaneseToThaiBtn.addEventListener('click', () => this.translateJapaneseToThai());
                this.listenThaiBtn.addEventListener('click', () => this.speakThaiText());
            }

            startRecordingJapanese() {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return;
                }
                if (this.isRecordingThai) { this.stopRecordingThai(); }
                if (this.recognitionJapanese && !this.isRecordingJapanese) {
                    this.recognitionJapanese.start();
                }
            }

            stopRecordingJapanese() {
                if (this.recognitionJapanese && this.isRecordingJapanese) {
                    this.recognitionJapanese.stop();
                }
                this.isRecordingJapanese = false;
                this.startJapaneseBtn.disabled = !this.geminiApiKey;
                this.stopJapaneseBtn.disabled = true;
                this.startJapaneseBtn.classList.remove('recording');
            }

            onJapaneseRecognitionStart() {
                this.isRecordingJapanese = true;
                this.updateStatus('กำลังฟัง (ญี่ปุ่น)... <span class="wave-animation"></span>', 'listening');
                this.startJapaneseBtn.disabled = true;
                this.stopJapaneseBtn.disabled = false;
                this.startJapaneseBtn.classList.add('recording');
                this.japaneseListenText.value = '';
                this.thaiTranslatedText.value = '';
                this.updateListenButtonStates();
            }

            onJapaneseRecognitionResult(event) {
                let finalTranscript = '';
                let interimTranscript = '';
                for (let i = event.resultIndex; i < event.results.length; i++) {
                    const transcript = event.results[i][0].transcript;
                    if (event.results[i].isFinal) {
                        finalTranscript += transcript;
                    } else {
                        interimTranscript += transcript;
                    }
                }
                this.japaneseListenText.value = finalTranscript + interimTranscript;
                if (finalTranscript) {
                    this.updateStatus('พบข้อความญี่ปุ่นแล้ว กำลังรอให้คุณพูดจบ...', 'success');
                }
                this.updateTranslateButtonStates();
            }

            onJapaneseRecognitionEnd() {
                this.stopRecordingJapanese();
                if (this.japaneseListenText.value.trim()) {
                    this.updateStatus('บันทึกเสียงญี่ปุ่นเสร็จสิ้น กำลังแปลภาษา...', 'processing');
                    this.translateJapaneseToThai();
                } else {
                    this.updateStatus('กดปุ่ม "เริ่มพูด (ญี่ปุ่น)" เพื่อเริ่มต้น', 'info');
                }
            }

            async translateJapaneseToThai() {
                this.updateStatus('กำลังแปลภาษาญี่ปุ่นเป็นไทย...', 'processing');
                this.translateJapaneseToThaiBtn.disabled = true;
                this.thaiTranslatedText.value = 'Translating...';
                this.listenThaiBtn.disabled = true;

                const result = await this.translateText(this.japaneseListenText.value, 'Japanese', 'Thai');
                this.thaiTranslatedText.value = result;

                if (result && !result.startsWith('Error:')) {
                    this.updateStatus('แปลภาษาญี่ปุ่นเป็นไทยเสร็จสิ้น', 'success');
                    this.speakThaiText();
                } else if (result.startsWith('Error:')) {
                    this.thaiTranslatedText.value = result;
                } else {
                    this.updateStatus('ไม่มีข้อความให้แปล หรือเกิดข้อผิดพลาด', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            speakThaiText() {
                const text = this.thaiTranslatedText.value.trim();
                if (!text || text.startsWith('Error:')) {
                    this.updateStatus('ไม่มีข้อความภาษาไทยให้อ่าน', 'info');
                    return;
                }

                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel();
                }

                this.speechSynthesisUtteranceThai = new SpeechSynthesisUtterance(text);
                this.speechSynthesisUtteranceThai.lang = 'th-TH';
                
                this.speechSynthesisUtteranceThai.onerror = (event) => {
                    console.error('Speech synthesis error (Thai):', event.error);
                    this.updateStatus(`ไม่สามารถอ่านออกเสียงภาษาไทยได้: ${event.error}`, 'error');
                };
                this.speechSynthesisUtteranceThai.onstart = () => {
                    this.updateStatus('กำลังอ่านออกเสียง (ไทย)...', 'processing');
                    this.listenThaiBtn.disabled = true;
                };
                this.speechSynthesisUtteranceThai.onend = () => {
                    this.updateStatus('อ่านออกเสียง (ไทย) เสร็จสิ้น', 'success');
                    this.listenThaiBtn.disabled = false;
                };

                window.speechSynthesis.speak(this.speechSynthesisUtteranceThai);
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            new BiDirectionalVoiceTranslator();
        });
    </script>
</body>
</html>
