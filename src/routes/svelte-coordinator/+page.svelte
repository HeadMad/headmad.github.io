<script>
  import Progress from './range.svelte'
  let value = $state([10, 80]);
</script>
<br><br>
  Value: {value}
  <Progress bind:value/>