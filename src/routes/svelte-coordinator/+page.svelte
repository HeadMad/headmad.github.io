<script>
  import Progress from './range.svelte'
  let value = $state([10, 20]);
</script>

  Value: {value}
  <Progress bind:value/>