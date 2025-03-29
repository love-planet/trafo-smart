<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Open Link</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: linear-gradient(to right bottom, rgb(26, 32, 44), rgb(74, 29, 150), rgb(91, 33, 182));
            color: #fff;
            font-family: Arial, sans-serif;
            height: 100vh;
            text-align: center;
        }
        #container {
            max-width: 600px;
            margin: 0 auto;
        }
        #image {
            max-width: 100%;
            height: auto;
            margin: 20px 0;
        }
        h1 {
            font-size: 3rem;
            margin: 0;
        }
        .button-container {
            margin-top: 20px;
        }
        button {
            padding: 1rem 2rem;
            font-size: 1.2rem;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 0.5rem;
        }
        button:hover {
            background-color: #45a049;
        }
        select {
            font-size: 1.2rem;
            padding: 0.5rem;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div id="container">
        <h1>Приветик</h1>
        
        <!-- Language Selection Dropdown -->
        <select id="languageSelect" onchange="changeLanguage()">
            <option value="en">English</option>
            <option value="ru">Русский</option>
        </select>

        <div class="button-container">
            <button id="openLinkBtn" onclick="openLink()">Open </button>
            <button id="copyLinkBtn" onclick="copyLink()">Copy </button>
        </div>
    </div>
 
    <script>
        const targetUrl = 'https://offers.affimelody.com/zeYpSX'; // Замените на нужный URL

        // Function to change button text based on language selection
        function changeLanguage() {
            const lang = document.getElementById('languageSelect').value;
            if (lang === 'ru') {
                document.getElementById('openLinkBtn').textContent = 'Открыть ссылку';
                document.getElementById('copyLinkBtn').textContent = 'Копировать ссылку';
            } else {
                document.getElementById('openLinkBtn').textContent = 'Open Link';
                document.getElementById('copyLinkBtn').textContent = 'Copy Link';
            }
        }

        // Initial language setup
        document.addEventListener("DOMContentLoaded", () => {
            const userLang = navigator.language || navigator.userLanguage; 
            if (userLang.includes('ru')) {
                document.getElementById('languageSelect').value = 'ru';
                changeLanguage();
            } else {
                document.getElementById('languageSelect').value = 'en';
                changeLanguage();
            }
        });

        const openLink = () => {
            const isAndroid = /Android/i.test(navigator.userAgent);
            const isIOS = /iPhone|iPad|iPod/i.test(navigator.userAgent);

            if (isAndroid) {
                let formattedUrl = targetUrl;
                if (!targetUrl.startsWith("https://") && !targetUrl.startsWith("http://")) {
                    formattedUrl = "https://" + targetUrl;
                }
                window.location.href = `intent://${formattedUrl.replace('https://', '')}#Intent;scheme=https;package=com.android.chrome;end`;
            } else if (isIOS) {
                window.location.replace(`x-safari-${targetUrl}`);
            } else {
                window.location.href = targetUrl;
            }
        };

        const copyLink = () => {
            navigator.clipboard.writeText(targetUrl).then(() => {
                alert('Link copied to clipboard!');
            }, (err) => {
                console.error('Failed to copy link: ', err);
            });
        };
    </script>
</body>
</html>
