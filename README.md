# PRODIGY-INFOTECH-LANDING-PAGE-TASK--02
HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="stopwatch">
        <div class="display" id="display">00:00:00</div>
        <div class="controls">
            <button id="start">Start</button>
            <button id="pause">Pause</button>
            <button id="reset">Reset</button>
            <button id="lap">Lap</button>
        </div>
        <div class="laps">
            <h2>Laps</h2>
            <ul id="lap-list"></ul>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>

CSS
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
    margin: 0;
}

.stopwatch {
    text-align: center;
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.display {
    font-size: 3em;
    margin-bottom: 20px;
}

.controls button {
    margin: 5px;
    padding: 10px 20px;
    font-size: 1em;
    cursor: pointer;
}

.laps {
    margin-top: 20px;
}

.laps ul {
    list-style: none;
    padding: 0;
}

.laps li {
    padding: 5px 0;
}

JAVASCRIPT

document.addEventListener('DOMContentLoaded', () => {
    let startTime, updatedTime, difference, tInterval, running = false, lapCount = 0;
    let hours = 0, minutes = 0, seconds = 0;
    const display = document.getElementById('display');
    const lapList = document.getElementById('lap-list');

    function startTimer() {
        if (!running) {
            startTime = new Date().getTime();
            tInterval = setInterval(getShowTime, 1);
            running = true;
        }
    }

    function getShowTime() {
        updatedTime = new Date().getTime();
        difference = updatedTime - startTime;

        hours = Math.floor((difference / (1000 * 60 * 60)) % 24);
        minutes = Math.floor((difference / (1000 * 60)) % 60);
        seconds = Math.floor((difference / 1000) % 60);

        hours = (hours < 10) ? "0" + hours : hours;
        minutes = (minutes < 10) ? "0" + minutes : minutes;
        seconds = (seconds < 10) ? "0" + seconds : seconds;

        display.innerHTML = hours + ":" + minutes + ":" + seconds;
    }

    function pauseTimer() {
        clearInterval(tInterval);
        running = false;
    }

    function resetTimer() {
        clearInterval(tInterval);
        running = false;
        hours = minutes = seconds = 0;
        display.innerHTML = "00:00:00";
        lapList.innerHTML = '';
        lapCount = 0;
    }

    function addLap() {
        if (running) {
            lapCount++;
            const li = document.createElement('li');
            li.textContent = `Lap ${lapCount}: ${display.textContent}`;
            lapList.appendChild(li);
        }
    }

    document.getElementById('start').addEventListener('click', startTimer);
    document.getElementById('pause').addEventListener('click', pauseTimer);
    document.getElementById('reset').addEventListener('click', resetTimer);
    document.getElementById('lap').addEventListener('click', addLap);
});
