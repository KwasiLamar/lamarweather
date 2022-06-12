<script>
	import './app.css';
	import { goto } from '$app/navigation';
	import axios from 'axios';
	let searchTerm = '';
	const searchCity = () => {
		if (searchTerm !== '') {
			goto('/search/' + searchTerm);
		}
	};
	import { onMount } from 'svelte';
	let lat = '';
	let long = '';
	let str = '';
	let condition_text = '';
	let temp_c;
	let temp_f;
	let icon;
	// import sunny from '$lib/assets/sunny.png';

	onMount(async () => {
		function getLocation() {
			if (navigator.geolocation) {
				navigator.geolocation.getCurrentPosition(showLocation);
			} else {
				console.log('Geolocation is not supported by this browser.');
			}
		}
		function showLocation(position) {
			lat = position.coords.latitude;
			long = position.coords.longitude;
			const options = {
				method: 'GET',
				url: 'https://weatherapi-com.p.rapidapi.com/current.json',
				params: { q: `${lat.toString()},${long.toString()}` },
				headers: {
					'X-RapidAPI-Key': 'dacd056670msh28c9d460fd44004p166d2bjsn88910eb48745',
					'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
				}
			};

			axios
				.request(options)
				.then(function (response) {
					console.log(response.data);
					str = `${response.data.location.name}, ${response.data.location.country}`;
					temp_c = response.data.current.temp_c;
					temp_f = response.data.current.temp_f;
					icon = response.data.current.condition.icon;
					condition_text = response.data.current.condition.text;
				})
				.catch(function (error) {
					console.error(error);
				});
			// console.log(lat, long);
		}
		getLocation();

		console.log(lat, long);
	});
</script>

<svelte:head>
	<title>Weather App</title>
</svelte:head>

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

<style>
</style>
