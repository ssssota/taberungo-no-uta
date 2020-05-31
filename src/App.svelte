<script>
	import { tick } from 'svelte';
	import TaberungoNoUta from './TaberungoNoUta.svelte';

	let active = true;
	function activeToggle() {
		active = !active;
	}
</script>

<main on:click={activeToggle}>
	<TaberungoNoUta {active} />
</main>

<style type="text/scss">
:global(body) {
	margin: 0;
	padding: 0;
	background: black;
}
main {
	width: 100vw;
	height: 100vh;
}
:global(.taberungo-no-uta) {
  /* center 16:9 display */
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100vw;
  height: 56.25vw;
  max-width: 177.78vh;
  max-height: 100vh;
}
</style>