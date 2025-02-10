<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personalized Study Timer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        #timer {
            font-size: 48px;
            margin: 20px;
        }
        button {
            font-size: 16px;
            padding: 10px;
            margin: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Personalized Study Timer</h1>
    <label>Study Time (minutes): <input type="number" id="studyTime" value="25"></label>
    <label>Break Time (minutes): <input type="number" id="breakTime" value="5"></label>
    <br><br>
    <button onclick="startTimer()">Start</button>
    <button onclick="resetTimer()">Reset</button>
    
    <h2 id="session">Session: Study</h2>
    <div id="timer">25:00</div>

    <script>
        let timeLeft, timer;
        let isStudySession = true;
        let studyTime = 25;
        let breakTime = 5;

        function startTimer() {
            clearInterval(timer);
            studyTime = parseInt(document.getElementById("studyTime").value);
            breakTime = parseInt(document.getElementById("breakTime").value);
            timeLeft = (isStudySession ? studyTime : breakTime) * 60;
            updateDisplay();
            timer = setInterval(countdown, 1000);
        }

        function countdown() {
            if (timeLeft <= 0) {
                isStudySession = !isStudySession;
                document.getElementById("session").innerText = isStudySession ? "Session: Study" : "Session: Break";
                startTimer();
                return;
            }
            timeLeft--;
            updateDisplay();
        }

        function updateDisplay() {
            let minutes = Math.floor(timeLeft / 60);
            let seconds = timeLeft % 60;
            document.getElementById("timer").innerText = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
        }

        function resetTimer() {
            clearInterval(timer);
            isStudySession = true;
            document.getElementById("session").innerText = "Session: Study";
            document.getElementById("timer").innerText = "25:00";
        }
    </script>
</body>
</html>
