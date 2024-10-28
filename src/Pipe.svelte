<!-- src/Pipe.svelte -->
<script>
  export let x;
  export let height;
  export let gap;

  import pipeImage from './pipe.png'; // Import the pipe image
</script>

<!-- Top Pipe -->
<img src="{pipeImage}" alt="pipe" class="pipe top" style="height: {height}px; left: {x}px" />

<!-- Bottom Pipe -->
<img src="{pipeImage}" alt="pipe" class="pipe bottom" style="height: calc(100% - {height + gap}px); top: {height + gap}px; left: {x}px" />

<style>
  .pipe {
    position: absolute;
    width: 60px; /* Adjust width to match the pipe image dimensions */
  }

  .top {
    transform: rotate(180deg); /* Flip the top pipe upside-down */
  }

  .bottom {
    /* The bottom pipe will be displayed as is */
  }
</style>
