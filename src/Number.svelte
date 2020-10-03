<script>
let text;
let result;
fetch("utils.gc.wasm")
        .then(response => response.arrayBuffer())
        .then(result => WebAssembly.instantiate(result))
        .then(wasmModule => {
          result = wasmModule.instance.exports.add_one(2);
        });

</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
{result}
</main>
