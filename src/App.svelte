<script>
  	import Map from './lib/Map.svelte'
	import Scroll from './lib/Scroll.svelte'
	import FlipCard from './lib/FlipCard.svelte'
</script>

<main>
	<!--
	<div class="container">
		<h2><i>The Double Threat of Heavy Rainfall and Sea Level Rise</i></h2>
	</div> -->

	<p>
		In September 2021, New York City's subway system flooded as remnants of Hurricane Ida dumped record-breaking rain. Streets 
		turned into rivers, subways into waterfalls. This wasn't a one-off event. Around the world, coastal cities are facing a 
		dangerous mix of rising sea levels and heavier rainfall, a consequence of climate change. Together, these forces overwhelm 
		infrastructure, causing deadly floods and long-term economic damage.
	</p>
	
	<p>
		Rising temperatures means rising seas. Warmer oceans cause ice sheets to melt, adding more water to the ocean. In fact, 
		between 1979 and 2021, the Arctic Ocean lost sea ice at an average of 31,100 square miles, an area the size of South Carolina, 
		per year. To add to this, climate change also supercharges the atmosphere, allowing it to hold more moisture. For every 1 
		Celsius increase in temperature, the atmosphere can hold 7 percent more water vapor. This leads to more intense rainfall, 
		increasing the risk of sudden, devastating floods. In coastal cities, this means floodwaters won't drain quickly — when rain 
		meets a higher sea level, streets stay underwater longer, only amplifying the damage.
	</p>

	<p>
		Some coastal cities are already facing this crisis head-on. Miami experiences “sunny day” flooding, where high tides push 
		seawater into streets, even on clear days. Jakarta, Indonesia is sinking so fast due to a mix of sea-level rise and groundwater 
		depletion that the country is moving its capital. In New York, heavy rainfall has repeatedly shut down the subway system, with 
		storm drains unable to handle the rush.
	</p>

	<p>
		The U.S. has many prominent coastal cities that remain at-risk for climate-induced emergencies. To better understand and prepare, 
		it is important to study weather trends over time.
	</p>

	<Scroll />

	<p>
		These disasters come with a hefty price tag. In the United States alone, flooding incidents cost an average of 4.5 billion 
		dollars per year in damages, with homes, businesses, and public infrastructure suffering. Insurance costs are skyrocketing, 
		with insurance companies even withdrawing their services from certain at-risk locations. Beyond the financial toll, there's 
		a human cost — people displaced, businesses lost, and communities disrupted. Without intervention, these events will become 
		more frequent, forcing cities to make difficult choices.
	</p>

	<p>
		Most coastal cities were built for a climate that is vastly different than today. Storm drains, levees, and pumps designed 
		for 20th-century weather patterns are overwhelmed by today's extreme conditions. As rainfall increases and sea levels rise, 
		these systems need costly upgrades. Governments, however, can be slow to act, whether due to funding issues or the sheer 
		scale of the problem. Without adaptation, cities risk severe climate vulnerabilities.
	</p>

	<p>
		In recent years, many cities are starting to invest in climate resilience. The Netherlands, famous for its flood management, 
		has implemented massive storm barriers and floating buildings. China's “sponge city” program focuses on green infrastructure 
		— parks, permeable pavement, and wetlands that absorb excess rain. In the U.S., cities like Boston are raising seawalls and 
		redesigning drainage systems. 
	</p>

	<p>
		For a more detailed look at how climate change affects the U.S., explore the time-series map illustration for any of several
		coastal cities.
	</p>

	<Map />
	<br>
	<p>
		While these changes are a big step in the right direction, without a focus on reducing greenhouse 
		gas emissions, the problem will only continue to worsen.
	</p>

	<p>
		Ignoring these risks will be far more expensive than preparing for them. Frequent flooding could make some cities unlivable, 
		displacing millions and reducing property values. Businesses that rely on stable infrastructure — ports, transit systems, and 
		power grids — could face repeated disruptions. As roads and utilities degrade, access to essential services like healthcare and 
		clean water could also be compromised. Without proactive investment, cities will spend more on disaster recovery than on 
		prevention, deepening financial and social instability.
	</p>

	<p>
		Smart policy and urban planning can reduce flood risks before disasters strike. Cities can update zoning laws to prevent 
		construction in high-risk areas, invest in better drainage systems, and require flood-resistant building designs. Governments 
		must also plan for long-term adaptation — whether through sea walls, elevated infrastructure, or even strategic relocation. 
		The challenge is balancing immediate economic interests with future resilience, as many policies still prioritize short-term 
		growth over climate preparedness.
	</p>

	<p>
		Flooding is just one symptom of a warming planet. Climate change is also driving extreme heat, prolonged droughts, and food 
		insecurity. Wildfires, hurricanes, and biodiversity loss are accelerating. Coastal flooding is a visible warning sign, but the 
		broader crisis affects every aspect of life. While adaptation is crucial, long-term solutions require cutting greenhouse gas 
		emissions and shifting to sustainable energy sources.
	</p>

	<div class="container">
		<h2><i>SURVIVING IN A WETTER WORLD</i></h2>
	</div>

	<p>
		Climate change can feel overwhelming, but solutions exist. From reducing personal carbon footprints to pushing for policy 
		change, individuals and communities have power. Investing in renewable energy, improving urban planning, and protecting 
		natural flood buffers like wetlands are all part of the solution. The fight against climate change isn't just about preventing 
		future disasters — it's about creating a safer, more sustainable world for everyone.
	</p>

	<p>
		Feel free to use the flashcards below to explore ways <b>you</b> can implement sustainability into your life 
		and help combat climate change.
	</p>

	<FlipCard />
</main>

<style>
	.container{
		max-width: 600px;
		margin: 0 auto;
	}
	
	h2 {
		color: #284057;
	}
	
	p {
		margin-left: auto;
		margin-right: auto;
		max-width: 600px;
	}
</style>