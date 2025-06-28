<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Walk&Talk Session Manager</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background-color: #f5f5f5;
            color: #333;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .app-container {
            max-width: 100%;
            margin: 0 auto;
            background-color: white;
            min-height: 100vh;
        }

        .header {
            background: linear-gradient(135deg, #0066cc 0%, #004499 100%);
            color: white;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .header h1 {
            font-size: 24px;
            font-weight: 600;
        }

        .tab-navigation {
            display: flex;
            background-color: #fff;
            border-bottom: 1px solid #e0e0e0;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
            color: #666;
        }

        .tab.active {
            color: #0066cc;
            border-bottom: 3px solid #0066cc;
        }

        .tab-content {
            display: none;
            padding: 20px;
            animation: fadeIn 0.3s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .session-info {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
        }

        .session-info h2 {
            font-size: 20px;
            margin-bottom: 15px;
            color: #0066cc;
        }

        .info-grid {
            display: grid;
            gap: 10px;
        }

        .info-item {
            display: flex;
            align-items: center;
            padding: 10px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .info-item i {
            margin-right: 10px;
            color: #0066cc;
        }

        .quick-note {
            background-color: #fff;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }

        .quick-note h3 {
            margin-bottom: 15px;
            color: #333;
        }

        .note-input {
            width: 100%;
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 10px;
            transition: border-color 0.3s ease;
        }

        .note-input:focus {
            outline: none;
            border-color: #0066cc;
        }

        .button-group {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn-primary {
            background-color: #0066cc;
            color: white;
        }

        .btn-secondary {
            background-color: #e0e0e0;
            color: #333;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-voice {
            background-color: #dc3545;
            color: white;
            width: 100%;
            margin-top: 10px;
        }

        .btn-voice.recording {
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }

        .notes-list {
            max-height: 400px;
            overflow-y: auto;
        }

        .note-item {
            background-color: #f8f9fa;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            border-left: 4px solid #0066cc;
        }

        .note-item .timestamp {
            font-size: 12px;
            color: #666;
            margin-bottom: 5px;
        }

        .note-item .note-text {
            font-size: 16px;
            line-height: 1.5;
        }

        .summary-section {
            background-color: #fff;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            margin-bottom: 20px;
        }

        .summary-section h3 {
            margin-bottom: 15px;
            color: #333;
        }

        .summary-textarea {
            width: 100%;
            min-height: 150px;
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            resize: vertical;
        }

        .action-items {
            list-style: none;
            padding: 0;
        }

        .action-item {
            background-color: #f8f9fa;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .action-item input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .action-item label {
            flex: 1;
            cursor: pointer;
        }

        .floating-timer {
            position: fixed;
            bottom: 80px;
            right: 20px;
            background-color: #0066cc;
            color: white;
            padding: 15px 20px;
            border-radius: 50px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            font-weight: 600;
            font-size: 18px;
        }

        .icon {
            width: 20px;
            height: 20px;
            display: inline-block;
        }

        @media (max-width: 375px) {
            .header h1 {
                font-size: 20px;
            }
            
            .tab {
                font-size: 14px;
                padding: 12px 5px;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="header">
            <h1>Walk&Talk Session</h1>
        </div>

        <div class="tab-navigation">
            <div class="tab active" onclick="switchTab('session')">Session</div>
            <div class="tab" onclick="switchTab('notes')">Anteckningar</div>
            <div class="tab" onclick="switchTab('summary')">Sammanfattning</div>
        </div>

        <!-- Session Tab -->
        <div id="session-tab" class="tab-content active">
            <div class="session-info">
                <h2>Pågående Session</h2>
                <div class="info-grid">
                    <div class="info-item">
                        <span class="icon">📅</span>
                        <span id="session-date"></span>
                    </div>
                    <div class="info-item">
                        <span class="icon">👥</span>
                        <span id="participants">0 deltagare</span>
                    </div>
                    <div class="info-item">
                        <span class="icon">📍</span>
                        <span>Walk&Talk Route</span>
                    </div>
                </div>
            </div>

            <div class="quick-note">
                <h3>Snabb anteckning</h3>
                <input type="text" class="note-input" id="quick-note-input" placeholder="Skriv en snabb anteckning...">
                <div class="button-group">
                    <button class="btn btn-primary" onclick="addQuickNote()">
                        <span class="icon">💾</span>
                        Spara
                    </button>
                    <button class="btn btn-secondary" onclick="clearQuickNote()">
                        <span class="icon">🗑️</span>
                        Rensa
                    </button>
                </div>
                <button class="btn btn-voice" id="voice-btn" onclick="toggleVoiceRecording()">
                    <span class="icon">🎙️</span>
                    <span id="voice-btn-text">Starta röstinspelning</span>
                </button>
                <p style="font-size: 12px; color: #666; margin-top: 10px; text-align: center;">
                    Rösttranskribering aktiverad för svenska 🇸🇪
                </p>
            </div>
        </div>

        <!-- Notes Tab -->
        <div id="notes-tab" class="tab-content">
            <div class="notes-list" id="notes-list">
                <!-- Notes will be dynamically added here -->
            </div>
        </div>

        <!-- Summary Tab -->
        <div id="summary-tab" class="tab-content">
            <div class="summary-section">
                <h3>Session sammanfattning</h3>
                <textarea class="summary-textarea" id="summary-text" placeholder="Skriv en sammanfattning av sessionen..."></textarea>
            </div>

            <div class="summary-section">
                <h3>Åtgärdspunkter</h3>
                <ul class="action-items" id="action-items">
                    <li class="action-item">
                        <input type="checkbox" id="action1">
                        <label for="action1">Exempel: Boka uppföljningsmöte</label>
                    </li>
                </ul>
                <button class="btn btn-primary" onclick="addActionItem()">
                    <span class="icon">➕</span>
                    Lägg till åtgärd
                </button>
            </div>

            <div class="summary-section">
                <h3>Dela sammanfattning</h3>
                <div class="button-group">
                    <button class="btn btn-primary" onclick="shareViaEmail()">
                        <span class="icon">📧</span>
                        E-post
                    </button>
                    <button class="btn btn-secondary" onclick="copyToClipboard()">
                        <span class="icon">📋</span>
                        Kopiera
                    </button>
                </div>
            </div>
        </div>

        <div class="floating-timer" id="timer">00:00</div>
    </div>

    <script>
        let notes = [];
        let isRecording = false;
        let startTime = Date.now();
        let timerInterval;

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('session-date').textContent = new Date().toLocaleDateString('sv-SE');
            startTimer();
            loadStoredData();
        });

        function switchTab(tabName) {
            // Hide all tabs
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });

            // Show selected tab
            document.getElementById(tabName + '-tab').classList.add('active');
            event.target.classList.add('active');
        }

        function startTimer() {
            timerInterval = setInterval(updateTimer, 1000);
        }

        function updateTimer() {
            const elapsed = Math.floor((Date.now() - startTime) / 1000);
            const minutes = Math.floor(elapsed / 60).toString().padStart(2, '0');
            const seconds = (elapsed % 60).toString().padStart(2, '0');
            document.getElementById('timer').textContent = `${minutes}:${seconds}`;
        }

        function addQuickNote() {
            const input = document.getElementById('quick-note-input');
            const noteText = input.value.trim();
            
            if (noteText) {
                const note = {
                    id: Date.now(),
                    text: noteText,
                    timestamp: new Date().toLocaleTimeString('sv-SE'),
                    type: 'text'
                };
                
                notes.push(note);
                input.value = '';
                updateNotesList();
                saveToLocalStorage();
                
                // Show feedback
                input.style.borderColor = '#28a745';
                setTimeout(() => {
                    input.style.borderColor = '#e0e0e0';
                }, 1000);
            }
        }

        function clearQuickNote() {
            document.getElementById('quick-note-input').value = '';
        }

        let recognition;
        let transcriptionText = '';
        
        // Initialize speech recognition
        function initSpeechRecognition() {
            if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                recognition = new SpeechRecognition();
                
                // Set Swedish language
                recognition.lang = 'sv-SE';
                recognition.continuous = true;
                recognition.interimResults = true;
                
                recognition.onresult = function(event) {
                    let finalTranscript = '';
                    let interimTranscript = '';
                    
                    for (let i = event.resultIndex; i < event.results.length; i++) {
                        const transcript = event.results[i][0].transcript;
                        if (event.results[i].isFinal) {
                            finalTranscript += transcript + ' ';
                        } else {
                            interimTranscript += transcript;
                        }
                    }
                    
                    if (finalTranscript) {
                        transcriptionText += finalTranscript;
                        // Update input field with ongoing transcription
                        document.getElementById('quick-note-input').value = transcriptionText + interimTranscript;
                    }
                };
                
                recognition.onerror = function(event) {
                    console.error('Speech recognition error:', event.error);
                    if (event.error === 'not-allowed') {
                        alert('Mikrofontillgång nekad. Gör så här:\n\n1. Kontrollera att webbläsaren har mikrofontillgång\n2. Ladda om sidan\n3. Tillåt mikrofon när frågan kommer\n\nOBS: Filen måste laddas via HTTPS (inte file://)');
                        isRecording = false;
                        const voiceBtn = document.getElementById('voice-btn');
                        const voiceBtnText = document.getElementById('voice-btn-text');
                        voiceBtn.classList.remove('recording');
                        voiceBtnText.textContent = 'Starta röstinspelning';
                    } else if (event.error === 'no-speech') {
                        // Continue listening
                        if (isRecording) {
                            try {
                                recognition.start();
                            } catch(e) {
                                // Already started
                            }
                        }
                    }
                };
                
                recognition.onend = function() {
                    if (isRecording) {
                        // Restart if still recording
                        recognition.start();
                    }
                };
                
                return true;
            }
            return false;
        }

        function toggleVoiceRecording() {
            const voiceBtn = document.getElementById('voice-btn');
            const voiceBtnText = document.getElementById('voice-btn-text');
            
            if (!isRecording) {
                if (!recognition && !initSpeechRecognition()) {
                    alert('Din webbläsare stödjer inte rösttranskribering. Prova Chrome, Edge eller Safari.');
                    return;
                }
                
                transcriptionText = '';
                document.getElementById('quick-note-input').value = '';
                
                voiceBtn.classList.add('recording');
                voiceBtnText.textContent = 'Stoppa inspelning';
                isRecording = true;
                
                try {
                    recognition.start();
                } catch (e) {
                    console.error('Could not start recognition:', e);
                }
            } else {
                stopVoiceRecording();
            }
        }

        function stopVoiceRecording() {
            const voiceBtn = document.getElementById('voice-btn');
            const voiceBtnText = document.getElementById('voice-btn-text');
            
            voiceBtn.classList.remove('recording');
            voiceBtnText.textContent = 'Starta röstinspelning';
            isRecording = false;
            
            if (recognition) {
                recognition.stop();
            }
            
            // Save the transcribed text as a note if there's content
            if (transcriptionText.trim()) {
                const note = {
                    id: Date.now(),
                    text: '🎙️ ' + transcriptionText.trim(),
                    timestamp: new Date().toLocaleTimeString('sv-SE'),
                    type: 'voice'
                };
                
                notes.push(note);
                updateNotesList();
                saveToLocalStorage();
                
                // Clear the input field
                document.getElementById('quick-note-input').value = '';
            }
        }

        function updateNotesList() {
            const notesList = document.getElementById('notes-list');
            
            if (notes.length === 0) {
                notesList.innerHTML = '<p style="text-align: center; color: #666; padding: 40px;">Inga anteckningar än</p>';
                return;
            }
            
            notesList.innerHTML = notes.map(note => `
                <div class="note-item">
                    <div class="timestamp">${note.timestamp}</div>
                    <div class="note-text">${note.text}</div>
                </div>
            `).reverse().join('');
        }

        function addActionItem() {
            const actionText = prompt('Skriv in ny åtgärdspunkt:');
            if (actionText) {
                const actionsList = document.getElementById('action-items');
                const newItem = document.createElement('li');
                newItem.className = 'action-item';
                newItem.innerHTML = `
                    <input type="checkbox" id="action${Date.now()}">
                    <label for="action${Date.now()}">${actionText}</label>
                `;
                actionsList.appendChild(newItem);
                saveToLocalStorage();
            }
        }

        function shareViaEmail() {
            const summary = document.getElementById('summary-text').value;
            const subject = `Walk&Talk Sammanfattning - ${new Date().toLocaleDateString('sv-SE')}`;
            const body = encodeURIComponent(summary || 'Ingen sammanfattning tillgänglig.');
            
            window.location.href = `mailto:?subject=${subject}&body=${body}`;
        }

        function copyToClipboard() {
            const summary = document.getElementById('summary-text').value;
            const actionItems = Array.from(document.querySelectorAll('.action-item label')).map(label => `- ${label.textContent}`).join('\n');
            
            const fullText = `Walk&Talk Sammanfattning\n${new Date().toLocaleDateString('sv-SE')}\n\n${summary}\n\nÅtgärdspunkter:\n${actionItems}`;
            
            navigator.clipboard.writeText(fullText).then(() => {
                alert('Sammanfattning kopierad!');
            });
        }

        function saveToLocalStorage() {
            const data = {
                notes: notes,
                summary: document.getElementById('summary-text').value,
                startTime: startTime
            };
            localStorage.setItem('walkTalkSession', JSON.stringify(data));
        }

        function loadStoredData() {
            const stored = localStorage.getItem('walkTalkSession');
            if (stored) {
                const data = JSON.parse(stored);
                notes = data.notes || [];
                document.getElementById('summary-text').value = data.summary || '';
                startTime = data.startTime || Date.now();
                updateNotesList();
            }
        }

        // Auto-save summary
        document.getElementById('summary-text').addEventListener('input', saveToLocalStorage);
    </script>
</body>
</html>
