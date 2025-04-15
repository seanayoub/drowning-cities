<script>
	import cardData from './carddata.json';

	// track the flip state of each card
	let displayCard = Array(cardData.length).fill(false);
	
	// toggle function only affecting the clicked card
	const toggleDisplay = (index) => {
		displayCard = displayCard.map((state, i) => (i === index ? !state : state))
	};
</script>

<main>
	<!-- Card Containers -->
	<div class="card-container">
		{#each cardData as item, index}
			<div class="card">
				<div class="flip-box">
				  <div class="flip-box-inner" class:flip={displayCard[index]}>
				    <div class="flip-box-front">
				      <h3>{item.title}</h3>
				    </div>
				    <div class="flip-box-back">
				      <p>{item.details}</p>
				    </div>
				  </div>
				</div>
			
				<div class="border" id="reveal">
					<div class="inner">
						<button on:click={() => toggleDisplay(index)}>LEARN MORE</button>
					</div>
				</div>
			</div>
		{/each}
	</div>
</main>

<style>
	/* grid container for rows and columns */
	.card-container {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 20px;
		justify-content: center;
		margin: 20px auto;
		max-width: 900px;
	}
	
	/* flip box container */
	.flip-box {
	  background-color: transparent;
	  width: 310px;
	  height: 270px;
	  perspective: 1000px;
	}
	
	/* position the front and back side */
	.flip-box-inner {
	  position: relative;
	  width: 100%;
	  height: 100%;
	  text-align: center;
	  transition: transform 0.8s;
	  transform-style: preserve-3d;
	}
	
	/* horizontal flip rule */
	.flip {
	  transform: rotateY(180deg);
	}
	
	/* position front and back side of card */
	.flip-box-front, .flip-box-back {
	  position: absolute;
	  width: 100%;
	  height: 100%;
	  -webkit-backface-visibility: hidden; /* safari */
	  backface-visibility: hidden;
	  border-radius: 15px;
	}
	
	/* style the front side */
	.flip-box-front {
	  background-color: #6EA4BF;
	  color: black;
	}
	
	/* style the back side */
	.flip-box-back {
	  display: flex;
	  align-items: center;
	  justify-content: center;
	  padding: 20px;
	  background-color: #B5B682;
	  color: black;
	  transform: rotateY(180deg);
	  text-align: center;
	  box-sizing: border-box;
	}

	/* style button containers */
	#reveal {
		text-align: center;
		margin-top: 5px;
	}

	/* style buttons*/
	button {
		padding: 8px 16px;
		border: none;
		background-color: #6EA4BF;
		color: white;
		cursor: pointer;
		font-size: 16px;
		border-radius: 5px;
	}

	button:hover {
		background-color: #284057;
	}

	/* stack cards vertically on mobile */
	@media (max-width: 768px) {
	  .card-container {
	    grid-template-columns: 1fr;
	    max-width: 100%;
	    gap: 15px;
	  }
	  .flip-box {
	    width: 90%;
	    margin: 0 auto;
	  }
	}
</style>