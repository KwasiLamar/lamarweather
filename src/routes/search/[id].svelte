<script>
	import { page } from '$app/stores';

	import axios from 'axios';

	let results = [];

	const options = {
		method: 'GET',
		url: 'https://weatherapi-com.p.rapidapi.com/search.json',
		params: { q: $page.params.id },
		headers: {
			'X-RapidAPI-Key': 'dacd056670msh28c9d460fd44004p166d2bjsn88910eb48745',
			'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
		}
	};

	axios
		.request(options)
		.then(function (response) {
			results = response.data;
			console.log(results);
		})
		.catch(function (error) {
			console.error(error);
		});
</script>

{#each results as city}
	<div class="wrapper">
		<a href="/weather/{$page.params.id}"><h1>{city.name}, {city.country}</h1></a>
	</div>
{/each}
