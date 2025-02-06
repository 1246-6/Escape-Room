<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Escape Room</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f3f3f3;
    }
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin-top: 20px;
    }
    #timer {
      font-size: 24px;
      margin: 10px 0;
    }
    #progress-bar {
      width: 300px;
      height: 20px;
      background-color: #ddd;
      margin-top: 20px;
    }
    #progress {
      height: 100%;
      background-color: #4caf50;
    }
    .puzzle {
      margin: 15px;
    }
    .hidden-clue {
      display: none;
      color: red;
    }
    .correct {
      color: green;
    }
    .incorrect {
      color: red;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>Escape Room</h1>

  <div id="timer">Time Left: <span id="time-left">30</span> seconds</div>
  
  <div id="progress-bar">
    <div id="progress" style="width: 0%"></div>
  </div>
  
  <div id="puzzle-1" class="puzzle">
    <p>What is 5 + 3?</p>
    <input type="text" id="answer-1">
    <button onclick="checkAnswer(1)">Submit</button>
    <div id="clue-1" class="hidden-clue">Hint: It's one more than 7.</div>
    <div id="result-1"></div>
  </div>

  <div id="puzzle-2" class="puzzle" style="display: none;">
    <p>What is the color of the sky?</p>
    <input type="text" id="answer-2">
    <button onclick="checkAnswer(2)">Submit</button>
    <div id="clue-2" class="hidden-clue">Hint: Think of daytime.</div>
    <div id="result-2"></div>
  </div>

  <div id="puzzle-3" class="puzzle" style="display: none;">
    <p>What is the capital of France?</p>
    <input type="text" id="answer-3">
    <button onclick="checkAnswer(3)">Submit</button>
    <div id="clue-3" class="hidden-clue">Hint: Famous for the Eiffel Tower.</div>
    <div id="result-3"></div>
  </div>

  <div id="win-message" style="display: none;">
    <h2>Congratulations! You've escaped!</h2>
  </div>
</div>

<script>
  let timeLeft = 30;
  let interval = setInterval(updateTimer, 1000);
  let progress = 0;

  function updateTimer() {
    if (timeLeft <= 0) {
      clearInterval(interval);
      alert("Time's up! You failed to escape.");
    } else {
      document.getElementById("time-left").innerText = timeLeft;
      timeLeft--;
    }
  }

  function checkAnswer(puzzleNumber) {
    let answer = document.getElementById(`answer-${puzzleNumber}`).value.toLowerCase();
    let correctAnswer = "";
    
    if (puzzleNumber === 1) {
      correctAnswer = "8";
    } else if (puzzleNumber === 2) {
      correctAnswer = "blue";
    } else if (puzzleNumber === 3) {
      correctAnswer = "paris";
    }

    if (answer === correctAnswer) {
      document.getElementById(`result-${puzzleNumber}`).innerText = "Correct!";
      document.getElementById(`result-${puzzleNumber}`).classList.add("correct");
      document.getElementById(`result-${puzzleNumber}`).classList.remove("incorrect");
      showNextPuzzle(puzzleNumber);
      increaseProgress();
    } else {
      document.getElementById(`result-${puzzleNumber}`).innerText = "Incorrect, try again!";
      document.getElementById(`result-${puzzleNumber}`).classList.add("incorrect");
      document.getElementById(`result-${puzzleNumber}`).classList.remove("correct");
      document.getElementById(`clue-${puzzleNumber}`).style.display = "block";
    }
  }

  function showNextPuzzle(currentPuzzle) {
    if (currentPuzzle === 1) {
      document.getElementById("puzzle-1").style.display = "none";
      document.getElementById("puzzle-2").style.display = "block";
    } else if (currentPuzzle === 2) {
      document.getElementById("puzzle-2").style.display = "none";
      document.getElementById("puzzle-3").style.display = "block";
    } else if (currentPuzzle === 3) {
      document.getElementById("puzzle-3").style.display = "none";
      document.getElementById("win-message").style.display = "block";
    }
  }

  function increaseProgress() {
    progress += 33.33;
    document.getElementById("progress").style.width = `${progress}%`;
  }
</script>

</body>
</html>
