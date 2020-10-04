<script>
  export let direction;
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

<div>Which way are you going? {direction}</div>
<div class="character">
  <img class="character-sprite" alt="hanny" src="images/hanny.png" />
</div>
