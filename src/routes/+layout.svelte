<script>
   let {children} = $props();
</script>

<nav>
  <a href="/">Home</a> |
  <a href="/faq">FAQ</a>|
  <a href="/contacts">Contacts</a>
</nav>

{@render children()}
