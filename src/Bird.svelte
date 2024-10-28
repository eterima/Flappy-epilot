<!-- src/Bird.svelte -->
<script>
  export let birdY;
  import birdImage from './bird.png'; // Import the bird image
</script>

<img src="{birdImage}" alt="bird" class="bird" style="top: {birdY}px" />

<style>
  .bird {
    position: absolute;
    width: 34px; /* Adjust based on your image dimensions */
    height: 24px; /* Adjust based on your image dimensions */
    left: 20px;
  }
</style>
