<script>
  import Game from "./Game.svelte";
  import Stats from "./Stats.svelte";
  import Surround from "./Surround.svelte";
  export let name;
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .game-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <Surround>
    <h1>Welcome to Hanny's {name}!</h1>
    <p>The Adventures of Hanny the Penguin.</p>
  </Surround>
  <div class="game-container">
    <Game />
  </div>
</main>
