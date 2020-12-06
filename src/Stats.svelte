<script>
  import { bounceInOut, bounceOut } from "svelte/easing";
  import { flip } from "svelte/animate";
  import Box from "./Box.svelte";
  const options = { delay: 200, duration: 500 };
  let list = [];
  let next = 1;
  function removeItem(number) {
    list = list.filter(n => n !== number);
  }
  function addItem() {
    list = [next++, ...list];
  }

  import { tweened, spring } from "svelte/motion";
  import { draw, blur, fade } from "svelte/transition";
  import { linear } from "svelte/easing";
  let height = 300;
  //const store = tweened(0, { duration: 1000 });
  const store = spring(0, { stiffness: 0.3, damping: 0.3 });
  $: store.set(height || 0);
  let opts = { duration: 1000, easing: linear };
  let show = false;
</script>

<style>
  .container {
    width: 55%;
    background: wheat;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;

    border: 3px dotted red;
  }

  button {
    border: 3px solid red;
    width: 60px;
    height: 30px;
  }
</style>

<div class="container">
  <button on:click={addItem}>Add</button>
  {#each list as n (n)}
    <div animate:flip={options} transition:blur={options}>
      <button on:click={() => removeItem(n)}>{n}</button>
    </div>
  {/each}
  <input type="number" min="0" max="100" bind:value={height} />
  <Box height={$store} />
</div>

<button on:click={() => (show = !show)}>Toggle</button>
{#if show}
  <h1 transition:draw={opts}>Hello Draw</h1>
  <h1 transition:blur={opts}>Hello Blur</h1>
{/if}
