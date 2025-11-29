<script>
  let search = $state("");
  $effect(() => {
    search = Object.fromEntries(new URLSearchParams(window.location.search));
  }); 
</script>
<h1>Home</h1>

<pre>
  {JSON.stringify(search, null, 2)}
</pre>