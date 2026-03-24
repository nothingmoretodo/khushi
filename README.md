# khushi
for u
<!DOCTYPE html>
<html>
<head>
    <title>Mini Game</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: linear-gradient(135deg, #000000, #1a1a2e);
            color: white;
            font-family: Arial;
            text-align: center;
        }

        #bgText {
            position: absolute;
            top: 40%;
            width: 100%;
            font-size: 40px;
            opacity: 0.88;
            letter-spacing: 2px;
        }

        #player {
            position: absolute;
            bottom: 10px;
            left: 50%;
            font-size: 30px;
        }

        .heart {
            position: absolute;
            font-size: 24px;
        }

        .floatingText {
            position: absolute;
            font-size: 14px;
            opacity: 0.4;
        }

        #endScreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: black;
            display: none;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        button {
            padding: 10px 20px;
            border: none;
            background: #ff4d6d;
            color: white;
            cursor: pointer;
            margin-top: 15px;
        }
    </style>
</head>
<body>

<div id="bgText">Grab my heart if you want me beside you</div>

<h2 id="score">Score: 0</h2>
<div id="player">😎</div>

<div id="endScreen">
    <h1 id="finalMsg"></h1>
    <button onclick="location.reload()">Play Again</button>
</div>

<script>
let player = document.getElementById("player");
let scoreText = document.getElementById("score");
let endScreen = document.getElementById("endScreen");
let finalMsg = document.getElementById("finalMsg");

let score = 0;
let playerX = window.innerWidth / 2;

let messages = [
    "This one felt like you 💖",
    "Don't miss this 😌",
    "Almost there...",
    "You're doing better than expected",
    "Careful… this matters 😉"
];

document.addEventListener("mousemove", (e) => {
    playerX = e.clientX;
    player.style.left = playerX + "px";
});

function createHeart() {
    let heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerText = "💖";
    heart.style.left = Math.random() * window.innerWidth + "px";
    heart.style.top = "0px";
    document.body.appendChild(heart);

    // floating message
    let text = document.createElement("div");
    text.classList.add("floatingText");
    text.innerText = messages[Math.floor(Math.random() * messages.length)];
    text.style.left = heart.style.left;
    text.style.top = "20px";
    document.body.appendChild(text);

    let fall = setInterval(() => {
        let top = parseInt(heart.style.top);
        heart.style.top = top + 5 + "px";
        text.style.top = (top + 20) + "px";

        let heartX = heart.offsetLeft;
        let playerRect = player.getBoundingClientRect();

        if (
            heartX > playerRect.left &&
            heartX < playerRect.right &&
            top > window.innerHeight - 60
        ) {
            score++;
            scoreText.innerText = "Score: " + score;
            heart.remove();
            text.remove();
            clearInterval(fall);
        }

        if (top > window.innerHeight) {
            heart.remove();
            text.remove();
            clearInterval(fall);
        }
    }, 30);
}

setInterval(createHeart, 800);

setTimeout(() => {
    endScreen.style.display = "flex";

    if (score > 10) {
        finalMsg.innerText = "You win… but you already had me 😏";
    } else {
        finalMsg.innerText = "Not bad… try again, I might still be yours 😉";
    }
}, 15000);
</script>

</body>
</html>
