<script lang="ts">
	import L, { point } from "leaflet";
	import { onMount } from "svelte";
	import * as d3 from "d3";

	let selectedCity = "Boston";
	let map;
	let circle;
	let data = [];
	let dates = [];
	let selectedIndex = 0;
	
	const cities = {
		Boston: { coords: [42.355, -71.056], file: "boston.csv" },
		Chicago: { coords: [41.878, -87.629], file: "chicago.csv" },
		Seattle: { coords: [47.606, -122.332], file: "seattle.csv" },
		SanDiego: { coords: [32.715, -117.161], file: "sandiego.csv" },
		Miami: { coords: [25.761, -80.191], file: "miami.csv" }
	};

	async function loadCityData() {
		const { coords, file } = cities[selectedCity];
		map.setView(coords, 13);

		data = await d3.csv(file, d => ({
			date: d.year,
			rain: +d.precipitation
		}));
		dates = data.map(d => d.date);
		
		const startDate = "2025";
		selectedIndex = data.findIndex(d => d.date === startDate);

		if (selectedIndex === -1) {
			console.error(`Start date ${startDate} not found in dataset.`);
			selectedIndex = 0;
		};

		if (circle) {
			map.removeLayer(circle);
		}
		updateCircle(selectedIndex);

		const point = data[selectedIndex]
		const year = parseInt(point.date)
		const rainfall = point.rain;
		const radius = 650 + (rainfall * 250);
		const label = year > 2024
			? `Projected Average Rainfall in ${year}: ${rainfall.toFixed(2)} mm`
			: `Average Rainfall in ${year}: ${rainfall.toFixed(2)} mm`;
		const center = map.getCenter();
		circle = L.circle(center, {
			radius,
			color: "skyblue",
			fillColor: "skyblue",
			fillOpacity: 0.5
		}).addTo(map);
		circle.bindPopup(label).openPopup();
	};

	function updateCircle(index) {
		selectedIndex = index;
		const point = data[selectedIndex];
		const rainfall = point.rain;
		const year = parseInt(point.date)

		const baseRadius = 650;
		const scaleFactor = 250;
		const radius = baseRadius + (rainfall * scaleFactor);

		let label = year > 2024
			? `Projected Average Rainfall in ${year}: ${rainfall.toFixed(2)} mm`
			: `Average Rainfall in ${year}: ${rainfall.toFixed(2)} mm`;

		if (circle) {
			circle.setRadius(radius);
			circle.setPopupContent(label);
		}
	}

	onMount(async () => {
		// initalize map
		map = L.map("map").setView(cities[selectedCity].coords, 13);
		L.tileLayer("https://api.maptiler.com/maps/dataviz/{z}/{x}/{y}.png?key=xStHG59ZZdy1t0NBL9KZ", {
			attribution:
				'<a href="https://www.maptiler.com/copyright/" target="_blank">&copy; MapTiler</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>',
			maxZoom: 18,
			tileSize: 512,
			zoomOffset: -1
    	}).addTo(map);
		loadCityData();
	});
</script>

<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
     integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY="
     crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
     integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo="
     crossorigin=""></script>
</svelte:head>

<main>
	<div class="select-container">
		<select bind:value={selectedCity} on:change={loadCityData}>
			{#each Object.keys(cities) as city}
				<option aria-label={city} value={city}>{city}</option>
			{/each}
		</select>
	</div>

	<div id="map"></div>

	{#if dates.length > 0}
		<div class="slider-container">
			<input
				aria-label="Slide with Arrows"
				type="range"
				min="0"
				max="{dates.length - 1}"
				bind:value={selectedIndex}
				on:input={(e) => updateCircle(+(e.target as HTMLInputElement).value)}
			/>
			<div class="slider-ticks">
				{#each [1950, 1960, 1970, 1980, 1990, 2000, 2010, 2020, 2030, 2040, 2050] as year}
					<span>{year}</span>
				{/each}
			</div>
		</div>
	{/if}
</main>

<style>
	#map { 
		height: 425px; 
		max-width: 750px;
		margin: auto;
		border-radius: 10px;
	}

	.select-container {
		max-width: 750px;
		margin: 1rem auto 0 auto;
		display: flex;
		justify-content: flex-end;
		padding: 0.4rem;
	}

	select {
		font-size: 1rem;
		padding: 0.5rem 1rem;
		border-radius: 8px;
		border: 2px solid #6EA4BF;
		background-color: white;
		color: #284057;
		transition: border-color 0.3s, box-shadow 0.3s;
	}

	select:focus {
		outline: none;
		border-color: #284057;
		box-shadow: 0 0 0 3px rgba(110, 164, 191, 0.3)
	}

	.slider-container {
		margin: 1rem auto;
		max-width: 750px;
		text-align: center;
	}

	input[type="range"] {
		appearance: none;
		-webkit-appearance: none;
		width: 100%;
		height: 10px;
		background: #B5B682;
		border-radius: 4px;
		outline: none;
		transition: background 0.3s;
		cursor: pointer;
		z-index: 2;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	input[type="range"]::-webkit-slider-thumb {
		appearance: none;
		-webkit-appearance: none;
		width: 20px;
		height: 20px;
		background: #6EA4BF;
		border-radius: 50%;
		cursor: pointer;
		z-index: 3;
		transition: background 0.3s ease;
	}

	input[type="range"]::-moz-range-thumb {
		appearance: none;
		width: 20px;
		height: 20px;
		background: #6EA4BF;
		border-radius: 50%;
		cursor: pointer;
		z-index: 3;
		transition: background 0.3s ease;
	}

	input[type="range"]:active::-webkit-slider-thumb {
		background: #284057;
		z-index: 3;
	}
	
	input[type="range"]:active::-moz-range-thumb {
		background: #284057;
		z-index: 3;
	}

	.slider-ticks {
		display: flex;
		justify-content: space-between;
		max-width: 100%;
		margin: 0.25rem auto 1rem auto;
		padding: 0 2px;
		font-size: 0.75rem;
		color: #555;
		user-select: none;
	}

	.slider-ticks span {
		position: relative;
	}
	
	.slider-ticks span::before {
		content: "";
		position: absolute;
		top: -9px;
		left: 50%;
		transform: translateX(-50%);
		width: 2px;
		height: 6px;
		background-color: #888;
		z-index: 1;
	}
</style>