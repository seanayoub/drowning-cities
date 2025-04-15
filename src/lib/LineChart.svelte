<script lang="ts">
	import { onMount, onDestroy } from "svelte";
	import * as d3 from "d3";

	export let index: number;

	let svgContainer;
	let svg;
	let xScale, yScale, line, color;
	let cityData = {};
	const cities = ["miami", "seattle", "boston", "chicago", "sandiego"];

	let yearRanges = [1975, 2000, 2025, 2050]; // matched to scroll steps

	async function loadData() {
		const loaded = await Promise.all(
			cities.map(city =>
				d3.csv(`${city}.csv`, d => ({
					year: +d.year,
					precipitation: +d.precipitation
				}))
			)
		);

		cities.forEach((city, i) => {
			cityData[city] = loaded[i];
		});
	}

	function drawChart() {
		const width = 600, height = 450, margin = { top: 20, right: 30, bottom: 30, left: 50 };
		svg = d3.select(svgContainer)
			.append("svg")
            .attr("viewBox", `0 0 ${width} ${height}`)
            .attr("preserveAspectRatio", "xMidYMid meet")
            .classed("responsive-svg", true);
			// .attr("width", width)
			// .attr("height", height);

		const g = svg.append("g").attr("transform", `translate(${margin.left},${margin.top})`);

		const allYears = cityData["miami"].map(d => d.year);
		const allValues = Object.values(cityData).flat();

		xScale = d3.scaleLinear()
			.domain(d3.extent(allYears))
			.range([0, width - margin.left - margin.right]);

		yScale = d3.scaleLinear()
			.domain([0, d3.max(allValues, d => d.precipitation)])
			.range([height - margin.top - margin.bottom, 0]);

		color = d3.scaleOrdinal(d3.schemeTableau10).domain(cities);

		line = d3.line()
			.x(d => xScale(d.year))
			.y(d => yScale(d.precipitation));

		g.append("g")
			.attr("transform", `translate(0, ${height - margin.top - margin.bottom})`)
			.call(d3.axisBottom(xScale).tickFormat(d3.format("d")));

		g.append("g").call(d3.axisLeft(yScale));

		// Initialize empty lines
		for (let city of cities) {
			g.append("path")
				.attr("class", `line-${city}`)
				.datum([])
				.attr("stroke", color(city))
				.attr("fill", "none")
				.attr("stroke-width", 2);
		}

        // Add legend
        const legend = svg.append("g")
            .attr("class", "legend")
            .attr("transform", `translate(${width - margin.right - 35}, ${margin.top - 20})`);

        cities.forEach((city, i) => {
            const legendRow = legend.append("g")
                .attr("transform", `translate(0, ${i * 20})`);

            legendRow.append("rect")
                .attr("width", 10)
                .attr("height", 10)
                .attr("fill", color(city));

            legendRow.append("text")
                .attr("x", 15)
                .attr("y", 10)
                .style("font-size", "12px")
                .style("fill", "white")
                .text(city.charAt(0).toUpperCase() + city.slice(1));
        });
	}

	function updateChart(stepIndex) {
		const cutoffYear = yearRanges[stepIndex];
		const g = svg.select("g");

		for (let city of cities) {
			const filtered = cityData[city].filter(d => d.year <= cutoffYear);
			g.select(`.line-${city}`)
				.datum(filtered)
				.transition()
				.duration(800)
				.attr("d", line);
		}
	}

	onMount(async () => {
		await loadData();
		drawChart();
		updateChart(index);
	});

	$: if (svg && Object.keys(cityData).length > 0) {
		updateChart(index);
	}

	onDestroy(() => {
		d3.select(svgContainer).selectAll("*").remove();
	});
</script>

<div bind:this={svgContainer}></div>