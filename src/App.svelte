<script>
	import { tick } from 'svelte';
	import TaberungoNoUta from './TaberungoNoUta.svelte';

	let taberungoElement;
	let active = false;
	function activeToggle() {
		active = !active;
		(active && taberungoElement)? taberungoElement.play(): taberungoElement.stop();
	}
</script>

<main on:click={activeToggle}>
	<TaberungoNoUta
		bind:this={taberungoElement}
	/>
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