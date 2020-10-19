<script>
  import { onMount } from "svelte";
  import Character from "./Character.svelte";
  let hanny;
  let map;
  let x = 0,
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

  onMount(() => {
    step();
  });

  const placeCharacter = () => {
    map.style.transform = `translate3d(${2 * x}px, ${-2 * y}px, 0)`;
  };

  const step = () => {
    placeCharacter();
    window.requestAnimationFrame(() => {
      step();
    });
  };
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

  div.camera {
    width: 400px;
    height: 400px;
    overflow: hidden;
    background: cornflowerblue;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .map :global(.character) {
    translate: translate3d(111px, 12px, 0);
  }
</style>

<svelte:window on:keydown|preventDefault={handleKeydown} />
<main>
  Chapter 1
  <div class="camera">
    <div class="map" bind:this={map}>
      <Character bind:this={hanny} {x} {y} direction={key} />
    </div>
  </div>
</main>
