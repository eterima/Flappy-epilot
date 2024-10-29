<!-- src/Game.svelte -->
<script>
  import { onMount } from 'svelte';
  import Bird from './Bird.svelte';
  import Pipe from './Pipe.svelte';

  let birdY = 250;
  let birdVelocity = 0;
  let pipes = [{ x: 400, height: 200 }];
  let score = 0;
  let gameOver = false;
  let gameStarted = false; // Track if the game has started

  const gravity = 0.5;
  const flapStrength = -10;
  const pipeGap = 150;

  const resetGame = () => {
    birdY = 250;
    birdVelocity = 0;
    pipes = [{ x: 400, height: 200 }];
    score = 0;
    gameOver = false;
    gameStarted = false; // Reset gameStarted to show "Ready?" again
  };

  const flap = () => {
    if (gameStarted && !gameOver) {
      birdVelocity = flapStrength;
    } else if (gameOver) {
      resetGame();
    }
  };

  const startGame = () => {
    gameStarted = true;
    gameOver = false;
    birdVelocity = flapStrength; // Start with an initial flap
  };

  const gameLoop = () => {
    if (!gameStarted || gameOver) return;

    birdY += birdVelocity;
    birdVelocity += gravity;

    // Update pipes
    pipes = pipes.map(pipe => ({ ...pipe, x: pipe.x - 5 }));
    
    // Generate new pipes and score points
    if (pipes[0].x < -60) {
      pipes.shift();
      pipes.push({ x: 400, height: Math.floor(Math.random() * (300 - pipeGap)) + 50 });
      score += 1;
    }

    // Collision detection
    pipes.forEach(pipe => {
      if (
        birdY < 0 || 
        birdY > 576 || 
        (pipe.x < 54 && pipe.x > 20 && (birdY < pipe.height || birdY > pipe.height + pipeGap))
      ) {
        gameOver = true;
      }
    });
  };

  onMount(() => {
    const interval = setInterval(gameLoop, 30);
    return () => clearInterval(interval);
  });
</script>

<div class="game" on:click={flap}>
  {#if !gameStarted}
    <!-- Show the "Ready?" text before the game starts -->
    <div class="ready" on:click={startGame}>Ready?</div>
  {:else}
    <!-- Game elements once game starts -->
    <Bird {birdY} />
    {#each pipes as { x, height }, index}
      <Pipe {x} {height} gap={pipeGap} key={index} />
    {/each}
    <div class="score">Score: {score}</div>
    {#if gameOver}
      <div class="game-over">Game Over! Click to Restart</div>
    {/if}
  {/if}
</div>

<style>
  /* Set up the background image */
  .game {
    position: relative;
    width: 400px;
    height: 600px;
    background-image: url('/src/background.png'); /* Ensure this path matches your image location */
    background-size: cover;
    background-position: center;
    overflow: hidden;
    margin: 0 auto;
    user-select: none;
  }

  .ready {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 36px;
    color: white;
    cursor: pointer;
  }

  .score {
    position: absolute;
    top: 10px;
    left: 10px;
    color: white;
    font-size: 24px;
    font-family: Arial, sans-serif;
  }

  .game-over {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: red;
    font-size: 36px;
    font-family: Arial, sans-serif;
  }
</style>
