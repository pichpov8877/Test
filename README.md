<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Do You Love Me?</title>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #9af2ff 0%, #9adaff 100%);
            overflow: hidden;
            touch-action: manipulation;
        }
        
        .container {
            text-align: center;
            padding: 20px;
            background-color: #ff9af5;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            max-width: 90%;
        }
        
        h1 {
            color: white;
            margin-bottom: 30px;
        }
        
        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        button {
            padding: 12px 25px;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }
        
        #yesBtn {
            background-color: #4CAF50;
            color: white;
            z-index: 1;
        }
        
        #noBtn {
            background-color: #f44336;
            color: white;
            transition: transform 0.2s ease;
        }
        
        #yesBtn:hover, #yesBtn:active {
            background-color: #45a049;
            transform: scale(1.05);
        }
        
        .love-page {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .love-page h1 {
            color: #white;
            font-size: 2.5em;
            margin-bottom: 20px;
            animation: heartbeat 1.5s infinite;
        }
        
        @keyframes heartbeat {
            0% { transform: scale(1); }
            25% { transform: scale(1.1); }
            50% { transform: scale(1); }
            75% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        .love-page img {
            width: 150px;
            height: 150px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <div class="container" id="questionPage">
        <h1>សុខមាន អូនព្រមត្រូវគ្នាវិញហេ៎ស 🥹🩷</h1>
        <div class="buttons">
            <button id="yesBtn">Yes</button>
            <button id="noBtn">No</button>
        </div>
    </div>
    
    <div class="container love-page" id="lovePage">
        <h1>យ៉េ•••😝🩷ព្រះនាងរបស់បងព្រមហើយ🥹🌷 </h1>
        <h2>បងស្រលាញ់អូន អូនមាន ព្រះនាងតូចរបស់បង😭🫶😚</h2>
        <img src="https://i.ibb.co/PvLLYSDK/orca-image-1234959183-jpeg.jpg" alt="<3">
        <p>អរគុណហើយណា៎ ដែលយល់ព្រម មនុស្សល្អរបស់បង😁🩷🤘</p>
    </div>

    <script>
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const questionPage = document.getElementById('questionPage');
        const lovePage = document.getElementById('lovePage');
        
        // When No button is clicked, make it run away
        noBtn.addEventListener('click', function(e) {
            e.preventDefault();
            
            // Get viewport dimensions
            const maxX = window.innerWidth - noBtn.offsetWidth - 20;
            const maxY = window.innerHeight - noBtn.offsetHeight - 20;
            
            // Generate random position that doesn't overlap with Yes button
            let newX, newY;
            const yesBtnRect = yesBtn.getBoundingClientRect();
            
            do {
                newX = Math.max(10, Math.random() * maxX);
                newY = Math.max(10, Math.random() * maxY);
            } while (
                newX + noBtn.offsetWidth > yesBtnRect.left && 
                newX < yesBtnRect.right && 
                newY + noBtn.offsetHeight > yesBtnRect.top && 
                newY < yesBtnRect.bottom
            );
            
            // Apply the new position with smooth transition
            noBtn.style.position = 'absolute';
            noBtn.style.left = `${newX}px`;
            noBtn.style.top = `${newY}px`;
            noBtn.style.transform = 'scale(0.9)';
            
            // Reset transform after animation
            setTimeout(() => {
                noBtn.style.transform = 'scale(1)';
            }, 200);
        });
        
        // When Yes button is clicked, show love page
        yesBtn.addEventListener('click', function() {
            questionPage.style.display = 'none';
            lovePage.style.display = 'block';
            
            // Add some confetti effect
            for (let i = 0; i < 50; i++) {
                createConfetti();
            }
        });
        
        // Simple confetti effect
        function createConfetti() {
            const confetti = document.createElement('div');
            confetti.style.position = 'fixed';
            confetti.style.width = '10px';
            confetti.style.height = '10px';
            confetti.style.backgroundColor = getRandomColor();
            confetti.style.borderRadius = '50%';
            confetti.style.left = Math.random() * 100 + 'vw';
            confetti.style.top = '-10px';
            confetti.style.zIndex = '1000';
            document.body.appendChild(confetti);
            
            const animation = confetti.animate([
                { top: '-10px', transform: 'rotate(0deg)' },
                { top: '100vh', transform: 'rotate(360deg)' }
            ], {
                duration: Math.random() * 3000 + 2000,
                easing: 'cubic-bezier(0.1, 0.8, 0.9, 1)'
            });
            
            animation.onfinish = () => confetti.remove();
        }
        
        function getRandomColor() {
            const colors = ['#ff6b88', '#ff8e53', '#4CAF50', '#2196F3', '#9C27B0'];
            return colors[Math.floor(Math.random() * colors.length)];
        }
    </script>
</body>
</html>
