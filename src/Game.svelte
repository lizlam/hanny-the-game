<script>
  import Character from "./Character.svelte";
  let x,
    y = 0;
  let key;
  let keyCode;
  const handleKeydown = event => {
    key = event.key;
    keyCode = event.keyCode;
    switch (key) {
      case "ArrowUp":
        y -= 2;
        break;
      case "ArrowDown":
        y += 2;
        break;
      case "ArrowLeft":
        x += 2;
        break;
      case "ArrowRight":
        x -= 2;
        break;
      default:
    }
  };
  $: y = y;
  $: x = x;
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  div.map {
    image-rendering: pixelated;
    background-image: url("/images/test.png");
    background-repeat: no-repeat;
    background-size: 100% auto;
    width: 900px;
    height: 900px;
    position: relative;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<svelte:window on:keydown|preventDefault={handleKeydown} />
<main>
  Chapter 1
  <div class="map">
    <Character {x} {y} direction={key} />
  </div>
</main>
