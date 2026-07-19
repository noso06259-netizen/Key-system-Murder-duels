<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JECLAU Key System</title>
    <!-- Tailwind CSS per un design ultra moderno -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&display=swap');
        body {
            font-family: 'Space Grotesk', sans-serif;
            background-color: #0b0b0e;
        }
        /* Animazione testo arcobaleno sincronizzata con il Menu Roblox */
        .rainbow-text {
            background-image: linear-gradient(to right, #ff007f, #00f0ff, #7f00ff, #ff007f);
            background-size: 400% auto;
            color: transparent;
            -webkit-background-clip: text;
            background-clip: text;
            animation: rainbow 8s linear infinite;
        }
        @keyframes rainbow {
            to { background-position: 400% center; }
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4 relative overflow-hidden">
    <!-- Cerchi sfocati di sfondo per effetto Cyberpunk -->
    <div class="absolute w-80 h-80 rounded-full bg-cyan-500/10 blur-3xl -top-10 -left-10"></div>
    <div class="absolute w-80 h-80 rounded-full bg-purple-500/10 blur-3xl -bottom-10 -right-10"></div>

    <div class="w-full max-w-md bg-[#0f0f14]/80 border border-[#23232d] p-8 rounded-2xl shadow-2xl backdrop-blur-md relative z-10">
        <!-- Logo Header -->
        <div class="text-center mb-8">
            <h1 class="text-3xl font-extrabold rainbow-text tracking-wider uppercase">BY JECLAU</h1>
            <p class="text-[#8c8c9e] text-xs mt-2 uppercase tracking-widest">Premium Key System</p>
        </div>

        <!-- Sezione Card Generatore -->
        <div class="space-y-6">
            <div class="bg-[#121218] border border-[#1c1c24] rounded-xl p-4 text-center">
                <span class="text-xs text-[#6e6e7d] uppercase font-bold block mb-2">Your Activation Key</span>
                <div id="key-display" class="text-cyan-400 font-bold tracking-widest text-sm break-all select-all select-none">
                    CLICK GENERATE KEY BELOW
                </div>
            </div>

            <!-- Contatore Scadenza Chiave -->
            <div class="flex justify-between items-center text-xs text-[#8c8c9e] px-1">
                <span>Key Validity:</span>
                <span class="font-bold text-purple-400" id="timer-display">Determining...</span>
            </div>

            <!-- Pulsanti di Controllo -->
            <div class="space-y-3">
                <button id="btn-generate" class="w-full py-3.5 bg-gradient-to-r from-cyan-500 to-blue-500 text-white font-bold rounded-xl shadow-lg shadow-cyan-500/20 hover:from-cyan-400 hover:to-blue-400 transition-all duration-300 transform active:scale-[0.98]">
                    Generate Key
                </button>
                <button id="btn-copy" class="w-full py-3 bg-[#161620] border border-[#2c2c3a] text-[#c8c8cd] font-medium rounded-xl hover:bg-[#1b1b28] hover:border-[#3a3a4c] transition-all duration-300">
                    Copy to Clipboard
                </button>
            </div>
        </div>

        <div class="text-center mt-8 text-[11px] text-[#525260] uppercase tracking-wider">
            Key rotates automatically every 6 hours
        </div>
    </div>

    <script>
        // Funzione per generare lo stesso identico Hash temporale sincronizzato con Roblox
        function getDeterministicKey(offsetBlocks = 0) {
            const unixTime = Math.floor(Date.now() / 1000);
            // 6 ore corrispondono a 21600 secondi
            const currentBlock = Math.floor(unixTime / 21600) + offsetBlocks;
            
            const salt = "JECLAU_SECRET_ROBLOX_KEY_2026";
            const combined = currentBlock.toString() + salt;
            
            // Algoritmo DJB2
            let hash = 5381;
            for (let i = 0; i < combined.length; i++) {
                hash = ((hash * 33) + combined.charCodeAt(i)) >>> 0;
            }
            
            // Algoritmo FNV-1a
            let hash2 = 2166136261;
            for (let i = combined.length - 1; i >= 0; i--) {
                hash2 = (hash2 ^ combined.charCodeAt(i)) >>> 0;
                hash2 = Math.imul(hash2, 16777619) >>> 0;
            }
            
            const hex1 = (hash >>> 0).toString(16).toUpperCase().padStart(8, '0');
            const hex2 = (hash2 >>> 0).toString(16).toUpperCase().padStart(8, '0');
            const hex3 = ((hash ^ hash2) >>> 0).toString(16).toUpperCase().padStart(8, '0');
            const hex4 = ((hash2 >>> 4) >>> 0).toString(16).toUpperCase().padStart(8, '0');
            
            return `JEC-${hex1}-${hex2}-${hex3}-${hex4}`;
        }

        // Calcola il tempo rimanente alla scadenza dello slot di 6 ore corrente
        function updateExpirationTimer() {
            const unixTime = Math.floor(Date.now() / 1000);
            const remainingSeconds = 21600 - (unixTime % 21600);
            
            const h = Math.floor(remainingSeconds / 3600);
            const m = Math.floor((remainingSeconds % 3600) / 60);
            const s = remainingSeconds % 60;
            
            const timeString = `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
            document.getElementById('timer-display').innerText = `Expires in ${timeString}`;
        }

        // Gestione Elementi del DOM
        const btnGenerate = document.getElementById('btn-generate');
        const btnCopy = document.getElementById('btn-copy');
        const keyDisplay = document.getElementById('key-display');

        btnGenerate.addEventListener('click', () => {
            const key = getDeterministicKey(0);
            keyDisplay.innerText = key;
            keyDisplay.classList.remove('select-none');
            keyDisplay.classList.add('text-green-400');
            keyDisplay.classList.remove('text-cyan-400');
        });

        btnCopy.addEventListener('click', () => {
            const textToCopy = keyDisplay.innerText;
            if (textToCopy && !textToCopy.includes("CLICK")) {
                navigator.clipboard.writeText(textToCopy).then(() => {
                    const originalText = btnCopy.innerText;
                    btnCopy.innerText = "Copied!";
                    btnCopy.classList.add('border-green-500/30', 'text-green-400');
                    setTimeout(() => {
                        btnCopy.innerText = originalText;
                        btnCopy.classList.remove('border-green-500/30', 'text-green-400');
                    }, 1500);
                });
            }
        });

        // Loop per il conto alla rovescia continuo
        setInterval(updateExpirationTimer, 1000);
        updateExpirationTimer();
    </script>
</body>
</html>
