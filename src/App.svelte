<script>
	import SearchCards from "./components/Search.svelte";
	
	export let name;
	
</script>
<main>
	<h1>Welcome to {name}!</h1>

	<SearchCards />

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	h1 {
		color: #ff3e00;
		
		font-size: 4em;
		font-weight: 100;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>