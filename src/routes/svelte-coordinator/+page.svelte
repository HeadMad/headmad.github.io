<script>
  import Progress from './range.svelte'
  let value = $state([10, 60]);
</script>

  Value: {value}
  <Progress bind:value/>