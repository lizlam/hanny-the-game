<script>
  import { onMount } from "svelte";
  import Character from "./Character.svelte";
  import Container from "./Container.svelte";
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

  const checkLocation = (x, y) => {
    if (x < -32 && -40 < x && y > 96 && y < 106) {
      console.log("Made it!");
    }
  };

  $: y = y;
  $: x = x;
  $: checkLocation(x, y);
  $: console.log({ x, y });

  onMount(() => {
    step();
  });

  let xOffset = 100;
  let yOffset = 100;
  const placeCharacter = () => {
    map.style.transform = `translate3d(${2 * x + xOffset}px, ${-2 * y +
      yOffset}px, 0)`;
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
    display: grid;
    grid-template-columns: 600px 1fr;
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

  div.stat {
    display: grid;
    grid-template-rows: 1fr 1fr;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<svelte:window on:keydown|preventDefault={handleKeydown} />
<main>
  <Container>
    <h2 slot="title">Chapter 1</h2>
    <div class="camera" slot="content">
      <div class="map" bind:this={map}>
        <Character bind:this={hanny} {x} {y} direction={key} />
      </div>
    </div>
  </Container>
  <div class="stat">
    <Container>
      <h2 slot="title">Progress</h2>
      <div slot="content">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="50"
          height="50"
          viewBox="0 0 79.72 45.59">
          <path
            d="M1,45.57c-1.33-.23-1.27-2.35.24-2C21.32,42.3,23.55-7.54,59.07,1,61,1.17,72.6,5,65.77,6c-8.3-1.31-14.51,6.83-16,14.18C47.16,30,55.64,39.8,65.47,40.11,68.91,41.25,78,39.88,79.72,42a1,1,0,0,1-1,.95c-8.81-.53-19,.75-25.9-5.88C42,27.82,47.46,7.76,60.75,3.89a26.77,26.77,0,0,0-10.46-1.4h0C24.22,3,20.9,46.63,1,45.57Z"
            fill="#010101" />
        </svg>
      </div>
    </Container>
    <Container class="inventory">
      <h2 slot="title">Inventory</h2>
      <div slot="content">Progress here ====></div>
    </Container>
  </div>
</main>
