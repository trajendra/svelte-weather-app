<script>
	import withQuery from "with-query"
	import Card from "./Card.svelte";
	import Button from "./UI/Button.svelte";
	import Inputbar from "./UI/Inputbar.svelte";
	export let result = "";
	export let formData = {
    	city: "",
  	};
  
  	let searchitems = [];
		
	async function handleSubmit(e) {
		e.preventDefault();
		await fetch(withQuery('https://api.openweathermap.org/data/2.5/weather', {
			q: formData.city,
			units: 'imperial',
			appid: '271d1234d3f497eed5b1d80a07b3fcd1',
		}))
		.then(resp => resp.json())
		.then(data => (result = data));

		const newSearchitem = {
			id: Math.random().toString(),
			temp: result["main"]["temp"],
			icon: result["weather"][0]["icon"],
			...formData
		};

		searchitems = [...searchitems, newSearchitem];

	}

	function formHandler(event) {
		formData[event.target.name] = event.target.value;	
	}

</script>
<main>

	<form on:submit={handleSubmit}>
		<Inputbar bind:value={formData.city} on:input={formHandler} />
		<Button type="submit" caption="Search" />
	</form>
	<section id="searchitems">
		{#each searchitems as searchitem}
			<Card city={searchitem.city} temp={searchitem.temp} icon={searchitem.icon} />
		{/each}
	</section>	

</main>


<style>

 
  section {
 	
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
  }

  @media (min-width: 768px) {
    section {
      grid-template-columns: repeat(6, 1fr);
    }
  }
</style>