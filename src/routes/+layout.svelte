<script>
  import {base} from '$app/paths';
   let {children} = $props();
</script>

<nav>
  <a href="/">Home</a> |
  <a href="/faq">FAQ</a> |
  <a href="/contacts">Contacts</a> |
  <a href="/some">Some</a>
</nav>

{@render children()}
