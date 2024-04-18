<script>
	import DetailedAnswers from "./DetailedAnswers.svelte";
	import answers from "$data/candidate-answers.csv";
	export let activeSlide;
	export let questions;
	import * as d3 from "d3";

	const candidates = [
		{ name: "Ebony Payne", last: "Payne", img: "ebony-payne.jpg" },
		{ name: "Kelvin Brown", last: "Brown", img: "kelvin-brown.jpg" },
		{ name: "Roscoe Grant Jr.", last: "Grant Jr.", img: "roscoe-grant-jr.jpg" },
		{ name: "Denise	Reed", last: "Reed", img: "denise-reed.jpg" },
		{ name: "Veda	Rasheed", last: "Rasheed", img: "veda-rasheed.jpg" },
		{
			name: "Villareal Johnson",
			last: "Johnson",
			img: "villareal-johnson.jpg"
		},
		{ name: "Ebbon Allen", last: "Allen", img: "ebbon-allen.jpg" },
		{
			name: "Eboni-Rose Thompson",
			last: "Thompson",
			img: "eboni-rose-thompson.jpg"
		},
		{ name: "Wendell Felder", last: "Felder", img: "wendell-felder.jpg" }
	];

	$: candidate = undefined;
	const setCandidate = (selCandidate) => (candidate = selCandidate);
	const selCandidate = (candidate) =>
		candidates.filter((d) => d.name === candidate)[0];

	$: matchPct = (candidate_last) => {
		let match = 0;
		questions.map((q, i) => {
			if (q.answer.toLowerCase() === answers[i][candidate_last].toLowerCase()) {
				match = match + 1;
			}
		});
		return d3.format(".0%")(+match / +questions.length);
	};

	let targetSection;

	function jumpToSection() {
		targetSection.scrollIntoView({ behavior: "smooth", block: "start" });
	}
	$: onCandidateSelect = (candidate) => {
		setCandidate(candidate.name);
		jumpToSection();
	};
</script>

<section>
	<div class="container">
		<div class="top">
			<div>
				<h3>Candidate matches</h3>
				<span
					>Click on a candidate's photo to get a detailed comparison of your
					answers.</span
				>
				<div class="results">
					{#each candidates as candidate}
						<button
							class="result"
							on:click={() => onCandidateSelect(candidate)}
						>
							<div class="photo">
								<img src="assets/candidates/{candidate.img}" alt="cat" />
							</div>
							<span class="name">{candidate.name}</span>
							<span class="match">{matchPct(candidate.last)}</span>
						</button>
					{/each}
				</div>
				<button>Take quiz again</button>
			</div>
		</div>

		<svg
			version="1.1"
			id="curved-border"
			xmlns="http://www.w3.org/2000/svg"
			xmlns:xlink="http://www.w3.org/1999/xlink"
			x="0px"
			y="0px"
			viewBox="0 0 1600 116.19"
			xml:space="preserve"
		>
			<path
				class="wave"
				d="M0.1,119.43V67.45c0,0,99.87,71.51,322.45,8.12c5.56-1.66,92.01-26.52,125.74-35.72
	c77.28-21.08,219.28-41.4,311.28-38.34c233,7.77,323.98,82.1,469.23,96.61c149.64,14.94,288.45-12.46,371.26-36.99v55.34L0.1,119.43
	z"
			/>
		</svg>
		<div class="bottom" id="results" bind:this={targetSection}>
			{#if candidate}
				<DetailedAnswers
					candidate={selCandidate(candidate)}
					{answers}
					{questions}
				/>
			{:else}
				<div class="placeholder">
					<span>Candidate's deatiled answers will appear here</span>
				</div>
			{/if}
		</div>
	</div>
</section>

<style>
	* {
		color: #fff;
	}
	path {
		fill: #c7871e;
	}
	.placeholder {
		height: 100vh;
		margin: 40px auto;
	}
	.placeholder span {
		position: relative;
		margin: 40px auto;
		max-width: fit-content;
		display: block;
		border: 1px dashed #fff;
		padding: 20px;
		border-radius: 5px;
	}
	img {
		object-position: top center;
		object-fit: cover;
		height: 100%;
		width: 100%;
	}
	button {
		background: rgba(0, 0, 0, 0);
	}
	.container {
		min-height: calc(100vh - 90px);
		display: grid;
		grid-template-rows: auto auto 1fr;
	}
	.top {
		padding: 0px 10px 40px;
		max-width: 800px;
		margin: 0px auto;
	}
	.bottom {
		background: #c7871e;
		padding: 0 10px;
		display: flex;
		align-items: center;
	}
	.results {
		display: grid;
		grid-template-columns: repeat(5, 1fr);
		column-gap: 0px;
		row-gap: 20px;
		align-items: flex-start;
		margin: 10px auto;
		width: 100%;
	}
	@media (max-width: 900px) {
		.results {
			grid-template-columns: repeat(4, 1fr);
		}
	}
	@media (max-width: 700px) {
		.results {
			grid-template-columns: repeat(3, 1fr);
		}
	}
	.match {
		display: block;
		text-align: center;
		font-weight: bold;
	}
	.result {
		display: block;
		text-align: center;
	}
	.result .photo:hover {
		border: 1px solid #000;
	}
	.result .photo {
		/* display: block;
		width: 100px;
		height: 100px;
		background: #ccc;
		border-radius: 10px;
		overflow: hidden;
		margin: 0 auto; */

		width: 100%;
		max-width: 200px;
		height: auto;
		aspect-ratio: 1 / 1; /* ⏹ a perfect square */
		background: #efefef;
		border-radius: 5px;
		overflow: hidden;
		margin-bottom: 8px;
	}
	.bar-container {
		height: 10px;
		width: 100%;
		background-color: #fff;
		position: relative;
	}
	.bar {
		position: absolute;
		width: 50%;
		height: 100%;
		background-color: #000;
	}
	.pct {
		text-align: right;
	}
</style>
