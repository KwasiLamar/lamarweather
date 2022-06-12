<script>
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	import axios from 'axios';

	let searchTerm = '';
	const searchCity = () => {
		if (searchTerm !== '') {
			goto('/search/' + searchTerm);
		}
	};

	// let lat = '';
	// let long = '';
	let str = '';
	let condition_text = '';
	let temp_c;
	let temp_f;
	let icon;

	const options = {
		method: 'GET',
		url: 'https://weatherapi-com.p.rapidapi.com/current.json',
		params: { q: $page.params.id },
		headers: {
			'X-RapidAPI-Key': 'dacd056670msh28c9d460fd44004p166d2bjsn88910eb48745',
			'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
		}
	};

	axios
		.request(options)
		.then(function (response) {
			temp_c = response.data.current.temp_c;
			temp_f = response.data.current.temp_f;
			icon = response.data.current.condition.icon;
			condition_text = response.data.current.condition.text;
			str = `${response.data.location.name}, ${response.data.location.country}`;
		})
		.catch(function (error) {
			console.error(error);
		});
</script>

<div class="wrapper">
	<div class="search">
		<input type="text" bind:value={searchTerm} placeholder="Search for a city..." />
		<button on:click={searchCity}>Search</button>
	</div>

	<h1>{str}</h1>
	<h2>Today</h2>
	<h3>{temp_c}°C / {temp_f}°F</h3>
	<h3>{condition_text}</h3>
	<img src={`https://${icon}`} alt="Sunny" />
</div>
