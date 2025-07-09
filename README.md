# Snake-Game
Snake Game


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Snake Game</title>
  <style>
    body {
      margin: 0;
      background-color: #000;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      color: white;
      font-family: Arial, sans-serif;
    }

    canvas {
      background-color: #111;
      border: 2px solid #fff;
    }

    h1 {
      margin-bottom: 20px;
    }
  </style>
</head>
<body>

<h1>🐍 Snake Game</h1>
<canvas id="gameCanvas" width="400" height="400"></canvas>

<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");

  const box = 20;
  const canvasSize = 400;

  let snake = [{ x: 9 * box, y: 10 * box }];
  let food = {
    x: Math.floor(Math.random() * (canvasSize / box)) * box,
    y: Math.floor(Math.random() * (canvasSize / box)) * box,
  };

  let direction = null;
  let score = 0;

  document.addEventListener("keydown", changeDirection);

  function changeDirection(e) {
    if (e.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
    else if (e.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
    else if (e.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
    else if (e.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Draw snake
    for (let i = 0; i < snake.length; i++) {
      ctx.fillStyle = i === 0 ? "#0f0" : "#0a0";
      ctx.fillRect(snake[i].x, snake[i].y, box, box);
    }

    // Draw food
    ctx.fillStyle = "#f00";
    ctx.fillRect(food.x, food.y, box, box);

    // Move snake
    let headX = snake[0].x;
    let headY = snake[0].y;

    if (direction === "UP") headY -= box;
    if (direction === "DOWN") headY += box;
    if (direction === "LEFT") headX -= box;
    if (direction === "RIGHT") headX += box;

    // Check game over
    if (
      headX < 0 || headX >= canvas.width || headY < 0 || headY >= canvas.height ||
      snake.some((segment, index) => index !== 0 && segment.x === headX && segment.y === headY)
    ) {
      clearInterval(game);
      alert("Game Over! Your Score: " + score);
      location.reload();
      return;
    }

    let newHead = { x: headX, y: headY };

    // Check food
    if (headX === food.x && headY === food.y) {
      score++;
      food = {
        x: Math.floor(Math.random() * (canvasSize / box)) * box,
        y: Math.floor(Math.random() * (canvasSize / box)) * box,
      };
    } else {
      snake.pop();
    }

    snake.unshift(newHead);
  }

  const game = setInterval(draw, 100);
</script>

</body>
</html>


https://github.com/atharvasangale7/Snake-Game/blob/e64d57a3b0cd80d1f985a5bcd99ece63303f2f1d/Screenshot%202025-07-09%20171541.png


