# SIMON GAME

Welcome to the Simon Game project! This is a fun and interactive memory game that challenges players to repeat a sequence of lights and sounds. The project demonstrates basic JavaScript functionalities, including DOM manipulation and event handling.

## Features

- Interactive gameplay with colored buttons
- Sound effects for each button press
- Score tracking to measure performance

## Getting Started

To get started with this project, follow these steps:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/Bhanu-partap-13/Simon-Game.git
    ```

2. **Navigate to the project directory**:
    ```bash
    cd Simon-Game
    ```

3. **Open `simon.html` in your web browser** to play the game.

## Usage

1. Watch the sequence of lights and sounds.
2. Repeat the sequence by clicking the buttons in the correct order.
3. Try to achieve the highest score without making mistakes!

## Preview

![Simon Game GIF](https://media.giphy.com/media/your-giphy-url.gif)

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simon Game</title>
    <link rel="stylesheet" href="simon.css">
</head>
<body>
    <h1>Simon Says Game</h1>
    <h2>Press any key to start the game</h2>
    <h3></h3>
    <div class="btn-contain 0er">
    <div class="line-one" >
    <div class="btn red" type="button" id="red">1</div>
    <div class="btn yellow" type="button" id="yellow">2</div>
</div>
    <div class="line-two">
    <div class="btn green" type="button" id="green">3</div>
    <div class="btn purp le" type="button" id="purple">4</div>
</div>
</div>
    <script src="simon.js"></script>
</body>
</html>

```
## js
```Javascript
let gameSeq = [];
let userSeq = [];
let btns = ["yellow", "red", "green", "purple"];

let started = false;
let level = 0;
let highscore = 1;

let h2 = document.querySelector("h2");
let h3 = document.querySelector("h3");

document.addEventListener("keypress", function () {
    if (!started) {
        console.log("Game Started");
        started = true;
        levelUp();
    }
});

function btnFlash(btn) {
    btn.classList.add("flashBtn");
    setTimeout(function () {
        btn.classList.remove("flashBtn");
    }, 500);
}

function userFlash(btn) {
    btn.classList.add("userFlash");
    setTimeout(function () {
        btn.classList.remove("userFlash");
    }, 500);
}

function levelUp() {
    userSeq = [];
    level++;
    if (level >= highscore) {
        highscore = level;
    }
    h2.innerText = `Level ${level}`;

    let randIdx = Math.floor(Math.random() * 4);
    let randColor = btns[randIdx];
    let randBtn = document.querySelector(`#${randColor}`);
    gameSeq.push(randColor);
    console.log(gameSeq);

    
    gameSeq.forEach((color, index) => {
        setTimeout(() => {
            let btn = document.querySelector(`#${color}`);
            btnFlash(btn);
        }, 650 * (index + 1));
    });
}

function checkAns(idx) {
    if(userSeq[idx] === gameSeq[idx]) {
        if (userSeq.length === gameSeq.length) {
            setTimeout(levelUp, 1000);
        }
    } else {
        h2.innerHTML = `Game Over! Your score was <b>${level}</b><br>Press any key to start again.`;
        h3.innerHTML = `Highest Score = ${highscore}`;
        document.querySelector("body").style.backgroundColor = "red";
        setTimeout(function () {
            document.querySelector("body").style.backgroundColor = "white";
        }, 1000);
        reset();
    }
}

function btnPress() {
    let btn = this;
    userFlash(btn);

    let userColor = btn.getAttribute("id");
    userSeq.push(userColor);

    checkAns(userSeq.length - 1);
}

let allBtns = document.querySelectorAll(".btn");
for (let btn of allBtns) {
    btn.addEventListener("click", btnPress);
}

function reset() {
    started = false;
    gameSeq = [];
    userSeq = [];
    level = 0;
}

document.addEventListener("keypress", function () {
    if (!started) {
        h2.innerText = "Press any key to start the game";
        document.querySelector("body").style.backgroundColor = "white";
    }
});
```
#CSS
```CSS
body{
    text-align: center;
    
}
.btn{
    height: 200px;
    width: 200px;
    border-radius: 20%;
    border: 10px solid black;
    margin:2.6rem;
}
.btn-container{
    display: flex;
    justify-content: center;
}
.yellow{
    background-color: yellow;
    background-color: #f99b45;
}
.red{
    background-color: red;
    background-color: #c9234a;
}
.green{
    background-color: green;
    background-color: #34b55d ;
}
.purple{
    background-color: purple;
    background-color: #7520ec;
}

.flashBtn{
    background-color: whitesmoke;
}

.userFlash{
    background-color: greenyellow;
}
```
