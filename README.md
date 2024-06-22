<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Paquet de Frites</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #dfa017, #d9c18f);
            font-family: Arial, sans-serif;
            overflow: hidden;
        }
        .background {
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        .emoji {
            position: absolute;
            font-size: 50px; /* Taille des émojis augmentée */
            animation: moveDiagonally 15s linear infinite;
        }
        @keyframes moveDiagonally {
            0% {
                transform: translate(0, 0);
            }
            100% {
                transform: translate(100vw, 100vh);
            }
        }
        @keyframes fall {
            0% {
                top: -100px;
            }
            100% {
                top: 100vh;
            }
        }
        .falling-image {
            position: absolute;
            width: 50px; /* Seule la largeur est définie pour conserver les proportions */
            animation: fall 5s linear;*/
        }
        .frame {
            background-color: white;
            padding: 40px; /* Taille de la frame augmentée */
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); /* Ombre ajoutée */
            text-align: center;
            position: relative;
            z-index: 1;
            border: 2px solid black; /* Ajout de la bordure noire */
            transition: transform 0.2s ease-in-out; /* Ajout de la transition */
        }
        .frame.animate {
            transform: scale(1.05); /* Taille de la frame augmentée légèrement */
        }
        .counter-container {
            font-size: 2em;
            margin-bottom: 20px;
        }
        button {
            background-color: #c72400;
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #8a1900;
        }
    </style>
</head>
<body>
    <div class="background" id="background"></div>
    <div class="frame" id="frame">
        <div class="counter-container" id="counterContainer">0</div>
        <button onclick="incrementCounter()">Ajouter une frite</button>
    </div>
    <script>
        const imagePaths = [
            '1.png',
            '2.png',
            '3.png',
            '4.png',
            '5.png',
            '6.png',
            '7.png',
            '8.png',
            '9.png',
            '10.png'
        ];

        let counter = 0;

        function incrementCounter() {
            counter++;
            document.getElementById('counterContainer').innerText = counter;
            createFallingImage();
            animateFrame();
        }

        function createFallingImage() {
            const background = document.getElementById('background');
            const img = document.createElement('img');
            img.src = imagePaths[Math.floor(Math.random() * imagePaths.length)];
            img.className = 'falling-image';
            img.style.left = Math.random() * 100 + 'vw';
            background.appendChild(img);

            setTimeout(() => {
                background.removeChild(img);
            }, 5000);
        }

        function animateFrame() {
            const frame = document.getElementById('frame');
            frame.classList.add('animate');
            setTimeout(() => {
                frame.classList.remove('animate');
            }, 200); // Durée de l'animation en millisecondes
        }

        setInterval(createEmoji, 500);
    </script>
</body>
</html>
