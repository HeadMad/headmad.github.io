<script>
  import Progress from './range.svelte'
  let value = $state([10, 20]);
</script>
<br><br>
  Value: {value}
  <Progress bind:value/>