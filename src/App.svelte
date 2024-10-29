<!-- src/App.svelte -->
<script>
  import Game from './Game.svelte';
</script>

<main>
  <Game />
</main>

<style>
  /* Import Google Font */
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

  /* Set the global font family */
  :global(body) {
    font-family: 'Press Start 2P', sans-serif;
  }

  main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #282c34;
  }
</style>
