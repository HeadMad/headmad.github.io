<script>
  import {base} from '$app/paths';
   let {children} = $props();
</script>

<nav>
  <a href="/">Home</a> |
  <a href="{base}/faq">FAQ</a>|
  <a href="{base}/contacts">Contacts</a>
</nav>

{@render children()}
