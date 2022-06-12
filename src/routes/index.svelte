<script>
	import './app.css';
	import sunny from '$lib/assets/sunny.png';
	console.log(sunny);
	print('HelloWOrld');
</script>

<svelte:head>
	<title>Weather App</title>
</svelte:head>

<div class="wrapper">
	<div class="search">
		<input type="text" placeholder="Search for a city..." />
		<button>Search</button>
	</div>

	<h1>Kumasi, Ghana</h1>
	<h2>Today</h2>
	<h3>23°C</h3>
	<img
		src="https://icons-for-free.com/iconfiles/png/512/sunny+weather+icon-1320196493554439865.png"
		alt="Sunny"
	/>
</div>

<style>
	.wrapper {
		margin: 2rem auto;
		padding: 1rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #333;
		border-radius: 1rem;
		width: 85%;
		text-align: center;
	}
	.wrapper h1,
	.wrapper h2,
	.wrapper h3 {
		margin-bottom: 1rem;
	}

	.search {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		margin: 2rem;
		width: 100%;
	}

	.search input {
		border: 1px solid #333;
		outline: none;
		border-top-left-radius: 1rem;
		border-bottom-left-radius: 1rem;
		padding: 1rem;
		font: 1rem 'Poppins', sans-serif;
	}

	.search button {
		border: 1px solid #333;
		outline: none;
		border-top-right-radius: 1rem;
		border-bottom-right-radius: 1rem;
		padding: 1rem;
		background-color: blue;
		color: #fff;
		font: 1rem 'Poppins', sans-serif;
	}

	img {
		width: 150px;
		height: auto;
		-webkit-filter: invert(100%); /* Safari/Chrome */
		filter: invert(100%);
	}
</style>
