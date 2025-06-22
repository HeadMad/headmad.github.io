<script>
  import {base} from '$app/paths';
   let {children} = $props();
   let arr = ['take', 'own', 'me']
</script>

<nav>
  <a href="/">Home</a> |
  <a href="/faq">FAQ</a> |
  <a href="/contacts">Contacts</a>
</nav>

{@render children()}
