<script>
  import {base} from '$app/paths';
   let {children} = $props();
</script>

<nav>
  <a href="/index.html">Home</a> |
  <a href="faq.html">FAQ</a>|
  <a href="contacts.html">Contacts</a>
</nav>

{@render children()}
