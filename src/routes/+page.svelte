<script>
	import Sudoku from './Sudoku.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<html lang="en">
<h1>Play Sudoku!</h1>
	<Sudoku/>
</html>

<style>

	h1 {
		width: 100%;
	}

</style>
