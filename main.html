import os
import http.server
import socketserver
import json
import google.generativeai as genai

# SETTINGS API
genai.configure(api_key=os.environ["GEMINI_API_KEY"])

# GENERATION
generation_config = {
    "temperature": 1,
    "top_p": 0.95,
    "top_k": 64,
    "max_output_tokens": 8192,
    "response_mime_type": "text/plain",
}

model = genai.GenerativeModel(
    model_name="gemini-1.5-flash",
    generation_config=generation_config,
)


class RequestHandler(http.server.SimpleHTTPRequestHandler):
    def do_GET(self):
        if self.path == '/':
            self.send_response(200)
            self.send_header('Content-type', 'text/html')
            self.end_headers()
            self.wfile.write(bytes(self.html(), 'utf-8'))
        else:
            self.send_error(404)

    def do_POST(self):
        if self.path == '/ask':
            content_length = int(self.headers['Content-Length'])
            post_data = self.rfile.read(content_length)
            data = json.loads(post_data)

            question = data.get('question')

            if not question:
                self.send_response(400)
                self.end_headers()
                self.wfile.write(bytes(json.dumps({
                    'error': 'Необходим параметр question.'}),
                    'utf-8'))
                return

            try:
                chat_session = model.start_chat(history=[])
                response = chat_session.send_message(question)

                if response:
                    answer = response.text
                else:
                    answer = 'Ошибка: пустой ответ от модели.'
            except Exception as e:
                answer = f'Ошибка при обращении к API: {str(e)}'

            # SEND RESPONSE
            response = {'answer': answer}
            self.send_response(200)
            self.send_header('Content-type', 'application/json')
            self.end_headers()
            self.wfile.write(bytes(json.dumps(response), 'utf-8'))
        else:
            self.send_error(404)  # Обработка неправильных путей

    def html(self):
        return """
        <!DOCTYPE html>
        <html lang="ru">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>AI Вопросы и Ответы</title>
            <style>
                :root {
                    --background-color: #1e1e1e;
                    --container-color: #2a2a2a;
                    --text-color: #e0e0e0;
                    --button-color: #444;
                    --input-background: #1e1e1e;
                    --circle-color-1: #ff6f91;
                    --circle-color-2: #6f92ff;
                }
                body.light-mode {
                    --background-color: #f7f7f7;
                    --container-color: #ffffff;
                    --text-color: #333;
                    --button-color: #ddd;
                    --input-background: #f1f1f1;
                    --circle-color-1: #ffcccb;
                    --circle-color-2: #add8e6;
                }
                body {
                    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                    background-color: var(--background-color);
                    color: var(--text-color);
                    margin: 0;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    min-height: 100vh;
                    padding: 20px;
                    position: relative;
                    overflow: hidden;
                }

                .background-circle {
                    content: "";
                    position: absolute;
                    border-radius: 50%;
                    opacity: 0.2;
                    pointer-events: none;
                    transition: transform 0.1s ease-out;
                }

                #circle1 {
                    width: 400px;
                    height: 400px;
                    background-color: var(--circle-color-1);
                    top: -150px;
                    left: -150px;
                }

                #circle2 {
                    width: 500px;
                    height: 500px;
                    background-color: var(--circle-color-2);
                    bottom: -200px;
                    right: -200px;
                }

                h1 {
                    font-weight: 600;
                    margin-bottom: 20px;
                }
                .container {
                    background-color: var(--container-color);
                    padding: 30px;
                    border-radius: 10px;
                    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4);
                    max-width: 600px;
                    width: 100%;
                    text-align: center;
                    position: relative;
                    z-index: 1;
                }

                textarea, input[type="text"] {
                    width: calc(100% - 20px);
                    margin: 10px 0;
                    padding: 10px;
                    border: 1px solid #444;
                    border-radius: 5px;
                    font-size: 1em;
                    background-color: var(--input-background);
                    color: var(--text-color);
                    outline: none;
                    transition: border-color 0.3s;
                }
                button {
                    background-color: var(--button-color);
                    color: var(--text-color);
                    padding: 12px 24px;
                    border: none;
                    border-radius: 5px;
                    cursor: pointer;
                    font-size: 1em;
                    font-weight: bold;
                    margin-top: 10px;
                    transition: background-color 0.3s, transform 0.2s ease-in-out;
                }
                button:hover {
                    background-color: #666;
                    transform: scale(1.05);
                }
                #theme-toggle {
                    background-color: transparent;
                    color: var(--text-color);
                    border: 1px solid var(--text-color);
                    margin-bottom: 10px;
                }
                #language-toggle {
                    margin-bottom: 10px;
                }
                h2 {
                    margin-top: 20px;
                }
                #answer {
                    background-color: var(--container-color);
                    padding: 15px;
                    border-radius: 5px;
                    font-size: 1em;
                    color: var(--text-color);
                    margin-top: 10px;
                    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.3);
                    text-align: left;
                }
            </style>
        </head>
        <body>
            <div id="circle1" class="background-circle"></div>
            <div id="circle2" class="background-circle"></div>

            <div class="container">
                <button id="theme-toggle" onclick="toggleTheme()">Переключить тему</button>
                <button id="language-toggle" onclick="toggleLanguage()">EN/RU</button>
                <h1 id="title">AI Вопросы и Ответы</h1>
                <textarea id="context" rows="5" placeholder="Введите контекст..."></textarea><br>
                <input type="text" id="question" placeholder="Введите ваш вопрос..."><br>
                <button onclick="askQuestion()">Спросить</button>
                <h2 id="answer-title">Ответ:</h2>
                <p id="answer"></p>
            </div>

            <script>
                function toggleTheme() {
                    document.body.classList.toggle('light-mode');
                }

                const translations = {
                    ru: {
                        title: 'AI Вопросы и Ответы',
                        placeholderContext: 'Введите контекст...',
                        placeholderQuestion: 'Введите ваш вопрос...',
                        askButton: 'Спросить',
                        answerTitle: 'Ответ:',
                    },
                    en: {
                        title: 'AI Questions & Answers',
                        placeholderContext: 'Enter context...',
                        placeholderQuestion: 'Enter your question...',
                        askButton: 'Ask',
                        answerTitle: 'Answer:',
                    }
                };
                let currentLang = 'ru';

                function toggleLanguage() {
                    currentLang = currentLang === 'ru' ? 'en' : 'ru';
                    const lang = translations[currentLang];
                    document.getElementById('title').innerText = lang.title;
                    document.getElementById('context').placeholder = lang.placeholderContext;
                    document.getElementById('question').placeholder = lang.placeholderQuestion;
                    document.querySelector('button[onclick="askQuestion()"]').innerText = lang.askButton;
                    document.getElementById('answer-title').innerText = lang.answerTitle;
                }

                async function askQuestion() {
                    const question = document.getElementById('question').value;
                    const context = document.getElementById('context').value;
                    const response = await fetch('/ask', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({ question, context })
                    });

                    const data = await response.json();
                    document.getElementById('answer').innerText = data.answer || 'Ответ не найден.';
                }
            </script>
        </body>
        </html>
        """


# START
PORT = 8000
with socketserver.TCPServer(("", PORT), RequestHandler) as httpd:
    print(f"Сервер запущен на порту {PORT}")
    httpd.serve_forever()
