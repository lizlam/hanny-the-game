<script>
  export let direction;
  export let x = 0;
  export let y = 0;
</script>

<style>

</style>

Which way are you going? {direction}
<svg
  tranform="translate({x},{y})"
  width="600"
  height="600"
  xmlns="http://www.w3.org/2000/svg">
  <!--
  with relative unit such as percentage, the visual size
  of the square looks unchanged regardless of the viewBox
  -->
  <rect {x} {y} width="32px" height="32px" />
</svg>
