<!-- src/App.svelte -->
<script>
  import Game from './Game.svelte';
</script>

<main>
  <Game />
</main>

<style>
  /* Import Google Font (e.g., 'Press Start 2P' for a retro style) */
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

  main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #282c34;
    font-family: 'Press Start 2P', sans-serif; /* Apply the font here */
  }
</style>
