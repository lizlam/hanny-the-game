<script>
  import { onMount, afterUpdate } from "svelte";
  export let direction;
  export let x;
  export let y;
  $: transform = `translate3d(${-3 * x}px, ${3 * y}px, 0)`;
</script>

<style>
  .character {
    width: 32px;
    height: 32px;
    overflow: hidden;
  }
  .character-sprite {
    animation: moveSprite 1s steps(4) infinite;
    image-rendering: pixelated;
  }

  @keyframes moveSprite {
    from {
      transform: translate3d(0px, 0, 0);
    }
    to {
      transform: translate3d(-100%, 0, 0);
    }
  }
</style>

<div class="character" style="transform: {transform}">
  <img class="character-sprite" alt="hanny" src="images/hanny.png" />
</div>
