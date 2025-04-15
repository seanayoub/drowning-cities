<script lang="ts">
	import Scroller from "@sveltejs/svelte-scroller";
	import LineChart from "./LineChart.svelte";

	let count;
	let index;
	let top = 0.1;
	let threshold = 0.33;
	let bottom = 0.9;

	// adjust 'bottom' based on screen width
	if (typeof window !== 'undefined') {
		const updateBottom = () => {
			if (window.innerWidth <= 600) {
				bottom = 0.45; // smaller on mobile
			} else {
				bottom = 0.9; // default for desktop
			}
		};
		updateBottom();
		window.addEventListener('resize', updateBottom);
	}
</script>

<main>
	<br>
	<Scroller {top} {threshold} {bottom} bind:count bind:index>
		<div slot="background" class="background">
			<LineChart {index} />
		</div>
		<div slot="foreground" class="foreground">
			<section><p>1975: Rainfall patterns vary considerable across U.S. cities. Places like Seattle experience more precipitation on average per year compared to cities like San Diego.</p></section>
			<section><p>2000: By the turn of the century, fluctuations in average rainfall remained the norm. However, all five of the cities displayed see a gradual increase in their trend line.</p></section>
			<section><p>2025: Precipitation levels continue to rise and fall unpredictably between cities. Miami and Chicago seem to experience an increase in average rainfall over this period while San Diego trends downward.</p></section>
			<section><p>2050: The projected data shows further instability in precipitation trends. Climate change isn't producing a single pattern - just more uncertainty.</p></section>
		</div>
	</Scroller>
</main>

<style>
	.background {
		background-color: rgba(20, 20, 20, 0.8);
		color: white;
		text-align: center;
		padding: 1rem;
		position: relative;
		margin-left: auto;
		margin-right: auto;
		max-width: 600px;
	}

	.foreground {
		pointer-events: none;
		margin-left: auto;
		margin-right: auto;
		max-width: 600px;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	section {
		min-height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
		padding: 2rem 0;
	}

	section p {
		background-color: rgba(0, 0, 0, 0.8);
		padding: 1rem;
		max-width: 300px;
		text-align: center;
		border: 1px solid white;
		border-radius: 8px;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
	}

	@media (max-width: 600px) {
		section {
			min-height: 40vh;
			padding: 1rem 0;
		}
		section p {
			max-width: 80vw;
			font-size: 0.95rem;
		}
	}
</style>