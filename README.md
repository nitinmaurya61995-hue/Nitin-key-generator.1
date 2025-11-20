<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neon Key Generator - Nitin DIGITAL MODS</title>
    <style>
        /* General Styles */
        body {
            font-family: 'Consolas', monospace; /* Techy font */
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background-color: #0c0022; /* Very Dark Blue/Purple */
            color: #f0f0f0;
            user-select: none;
        }

        .container {
            background-color: #1c0032;
            padding: 35px 50px;
            border-radius: 15px;
            box-shadow: 0 0 50px rgba(100, 50, 255, 0.5); /* Main container glow (Purple) */
            text-align: center;
            border: 2px solid #6432ff;
            max-width: 90%;
            width: 450px;
        }

        h2 {
            color: #fff;
            text-shadow: 0 0 10px #ff32e4, 0 0 20px #ff32e4; /* Magenta Header Glow */
            margin-bottom: 30px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* --- Key Generator Section --- */

        .neon-btn {
            background: none;
            border: 2px solid #32ffc8; /* Cyan/Green Border */
            color: #f0f0f0;
            padding: 14px 30px;
            font-size: 1.1em;
            text-transform: uppercase;
            letter-spacing: 3px;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.3s ease;
            box-shadow: 0 0 10px #32ffc8, 0 0 20px #32ffc8; /* Button Glow */
            margin-bottom: 25px;
            outline: none;
            width: 100%;
            font-weight: bold;
        }

        .neon-btn:hover {
            background-color: #32ffc8;
            color: #0c0022;
            box-shadow: 0 0 25px #32ffc8, 0 0 50px #32ffc8;
        }

        #keyDisplay {
            min-height: 40px;
            padding: 15px;
            margin-top: 15px;
            border: 2px dashed #ffff32; /* Yellow Dashed Border */
            border-radius: 8px;
            font-size: 1.4em;
            font-weight: bold;
            color: #ffff32; /* Key Text Color (Yellow) */
            text-shadow: 0 0 5px #ffff32;
            display: flex;
            justify-content: center;
            align-items: center;
            word-break: break-all;
            background-color: #150030;
        }

        #copyBtn {
            background-color: #ff32e4; /* Magenta Copy Button */
            color: #0c0022;
            border: none;
            padding: 8px 15px;
            font-size: 0.9em;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
            display: none;
            margin-left: 10px;
            font-weight: bold;
        }

        #copyBtn:hover {
            background-color: #ff64f0;
        }

        .key-row {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 25px;
        }

        #alertMessage {
            color: #32ffc8;
            font-size: 1.1em;
            margin-top: 10px;
            opacity: 0;
            transition: opacity 0.3s ease;
            min-height: 20px;
        }
        
        /* --- Social Links Section --- */
        .social-links {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #333;
            display: flex;
            justify-content: space-around;
        }
        
        .social-btn {
            border: 2px solid;
            padding: 10px 15px;
            font-size: 1em;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
            border-radius: 5px;
            transition: all 0.3s ease;
            margin: 0 5px;
            outline: none;
            text-decoration: none;
            display: inline-block;
            color: #f0f0f0;
            font-weight: bold;
        }

        /* Styles for tracking clicks */
        .youtube-btn {
            border-color: #ff0000; /* Red */
            box-shadow: 0 0 10px #ff0000;
        }
        .youtube-btn.clicked {
            background-color: #ff0000;
            color: white;
            box-shadow: 0 0 15px #ff0000;
        }
        
        .youtube-btn:hover:not(.clicked) {
            background-color: #ff3333;
        }

        .telegram-btn {
            border-color: #0088cc; /* Blue */
            box-shadow: 0 0 10px #0088cc;
        }
        .telegram-btn.clicked {
            background-color: #0088cc;
            color: white;
            box-shadow: 0 0 15px #0088cc;
        }

        .telegram-btn:hover:not(.clicked) {
            background-color: #33aaff;
        }
        
        /* --- Footer --- */
        .footer {
            margin-top: 30px;
            color: #6432ff;
            text-shadow: 0 0 5px #6432ff;
            font-size: 0.9em;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>🔑 Neon Key Generator 🔑</h2>
        
        <button class="neon-btn" onclick="generateKey()">
            Generate Key
        </button>

        <div class="key-row">
            <div id="keyDisplay">
                Your Key Will Appear Here...
            </div>
            <button id="copyBtn" onclick="copyKey()">Copy</button>
        </div>
        
        <div id="alertMessage"></div>
        
        <div class="social-links">
            <a id="ytLink" href="https://youtube.com/@sanatanigamer90?si=8mn1CMbo-2lUBam" target="_blank" 
               class="social-btn youtube-btn" onclick="trackClick('yt')">
                Open YouTube
            </a>
            
            <a id="tgLink" href="https://t.me/+MVN6iStjmxIxNTBl" target="_blank" 
               class="social-btn telegram-btn" onclick="trackClick('tg')">
                Open Telegram
            </a>
        </div>

    </div>
    
    <div class="footer">
        Powered by Nitin MODS
    </div>

    <script>
        // JavaScript Functions
        const targetKey = 'Nitin DIGITAL MODS';
        const keyDisplay = document.getElementById('keyDisplay');
        const copyBtn = document.getElementById('copyBtn');
        const alertMessage = document.getElementById('alertMessage');
        const defaultText = 'Your Key Will Appear Here...';
        
        // --- Key Tracking Flags ---
        let ytClicked = false;
        let tgClicked = false;
        
        const ytLink = document.getElementById('ytLink');
        const tgLink = document.getElementById('tgLink');

        function trackClick(source) {
            // Set the flag based on the clicked link
            if (source === 'yt') {
                ytClicked = true;
                ytLink.classList.add('clicked');
            } else if (source === 'tg') {
                tgClicked = true;
                tgLink.classList.add('clicked');
            }
            
            // Clear previous alerts
            alertMessage.textContent = '';
            alertMessage.style.opacity = '0';
        }

        function generateKey() {
            // Check if both links have been clicked
            if (ytClicked && tgClicked) {
                // 1. Display the key
                keyDisplay.textContent = targetKey;

                // 2. Show the Copy button
                copyBtn.style.display = 'inline-block';

                // 3. Inform the user
                alertMessage.textContent = 'Key Generated! You can now copy it.';
                alertMessage.style.opacity = '1';

            } else {
                // Display error message
                keyDisplay.textContent = 'Verification Required...';
                copyBtn.style.display = 'none';
                
                let missing = [];
                if (!ytClicked) missing.push('YouTube');
                if (!tgClicked) missing.push('Telegram');
                
                alertMessage.textContent = `❌ Please Open the ${missing.join(' and ')} Link${missing.length > 1 ? 's' : ''} First!`;
                alertMessage.style.opacity = '1';
                
                // Hide the error message after a few seconds
                setTimeout(() => {
                    alertMessage.style.opacity = '0';
                    keyDisplay.textContent = defaultText;
                }, 4000);
            }
        }

        function copyKey() {
            // Ensure the key is generated before copying
            if (keyDisplay.textContent === targetKey) {
                // 1. Copy the key to clipboard
                navigator.clipboard.writeText(targetKey).then(() => {
                    // 2. Show success message
                    alertMessage.textContent = '✅ Key Copied: ' + targetKey;
                    alertMessage.style.opacity = '1';

                    // 3. Reset the state after copying
                    setTimeout(() => {
                        alertMessage.style.opacity = '0';
                        keyDisplay.textContent = defaultText;
                        copyBtn.style.display = 'none';
                        
                        // Reset verification status for next time (optional)
                        // ytClicked = false;
                        // tgClicked = false;
                        // ytLink.classList.remove('clicked');
                        // tgLink.classList.remove('clicked');
                    }, 3000);

                }).catch(err => {
                    alertMessage.textContent = '❌ Copy Failed! Please copy manually.';
                    alertMessage.style.opacity = '1';
                });
            } else {
                 alertMessage.textContent = 'Please Generate Key First!';
                 alertMessage.style.opacity = '1';
            }
        }
    </script>

</body>
</html>
