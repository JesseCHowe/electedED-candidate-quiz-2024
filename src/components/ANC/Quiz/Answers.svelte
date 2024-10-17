<script>
	import DetailedAnswers from "./DetailedAnswers.svelte";
	import ward7Answers from "$data/anc/ward-7-answers.csv";
	import ward8Answers from "$data/anc/ward-8-answers.csv";
	export let activeSlide;
	export let questions;
	export let ward;
	import * as d3 from "d3";

	const ward8Candidates = [
		{ name: "Rev. Wendy Hamilton", last: "Hamilton" },
		{ name: "Patrice Lancaster", last: "Lancaster" },
		{ name: "Elizabeth Carter", last: "Carter" },
		{ name: "Marcus	Hickman", last: "Hickman" },
		{ name: "Scott Thach", last: "Thach" },
		{ name: "Gregory White", last: "White" },
		{ name: "Tom Donohue", last: "Donohue" },
		{ name: "Commissioner Duane Moody", last: "Moody" },
		{ name: "Deborah Wells", last: "Wells" },
		{ name: "Tomora Redman", last: "Redman" }
	];

	const ward7Candidates = [
		{ name: "Stanley Monickam", last: "Monickam" },
		{ name: "Caprice Casson", last: "Casson" },
		{ name: "Ashley Renee Ruff", last: "Ruff" },
		{ name: "Carlos	Richardson", last: "Richardson" },
		{ name: "Patricia Stamper", last: "Stamper" },
		{ name: "Dev Myers", last: "Myers" },
		{ name: "Patricia Williams", last: "Williams" },
		{ name: "Kimory	Orendoff", last: "Orendoff" },
		{ name: "Travis Swanson", last: "Swanson" },
		{ name: "John Adams", last: "Adams" }
	];

	let candidates;
	let answers;
	$: candidate = undefined;
	$: {
		if (+ward === 7) {
			answers = ward7Answers;
			candidates = ward7Candidates;
			candidate = undefined;
		}
		if (+ward === 8) {
			answers = ward8Answers;
			candidates = ward8Candidates;
			candidate = undefined;
		}
	}

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
		return +match / +questions.length;
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
				<div class="lead">
					<h3>Candidate matches</h3>
					<span
						>Click on a candidate's photo to get a detailed comparison of your
						answers. All running candidates were sent a questionnaire. Those
						candidates who replied are displayed below.</span
					>
				</div>

				<div class="results">
					{#each candidates.sort((a, b) => {
						return matchPct(a.last) > matchPct(b.last) ? -1 : 1;
					}) as candidate}
						<button
							class="result"
							on:click={() => onCandidateSelect(candidate)}
						>
							<i class="plus">
								<svg
									xmlns="http://www.w3.org/2000/svg"
									width="20px"
									height="20px"
									viewBox="0 0 24 24"
									><path
										fill="#fff"
										d="M11 17h2v-4h4v-2h-4V7h-2v4H7v2h4zm1 5q-2.075 0-3.9-.788t-3.175-2.137T2.788 15.9T2 12t.788-3.9t2.137-3.175T8.1 2.788T12 2t3.9.788t3.175 2.137T21.213 8.1T22 12t-.788 3.9t-2.137 3.175t-3.175 2.138T12 22"
									/></svg
								>
							</i>
							<span class="name">{candidate.name}</span>
							<span class="match"
								>{d3.format(".0%")(matchPct(candidate.last))}</span
							>
							<div class="bar-container">
								<div
									class="bar"
									style="width: {d3.format('.0%')(matchPct(candidate.last))}"
								/>
							</div>
						</button>
					{/each}
				</div>
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
	.wards {
		display: grid;
		grid-template-columns: 1fr 1fr;
		max-width: fit-content;
		margin: 0 auto;
		column-gap: 10px;
	}
	.wards button {
		padding: 10px;
		border-radius: 10px;
	}
	.wards button.active {
		font-weight: bold;
	}
	* {
		color: #000;
	}
	.lead > * {
		color: #fff;
	}
	h3 {
		margin: 0;
	}
	path {
		fill: #88bcd2;
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
		border: 1px dashed #000;
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
	.top span {
		max-width: 600px;
		display: block;
	}
	.top .coming-soon {
		margin-top: 20px;
		text-align: right;
		max-width: 100%;
	}
	.bottom {
		background: #88bcd2;
		padding: 0 10px;
		display: flex;
		align-items: center;
	}
	.results {
		display: grid;
		row-gap: 5px;
		/* grid-template-columns: repeat(5, 1fr); */
		column-gap: 0px;
		align-items: flex-start;
		margin: 10px auto;
		width: 100%;
	}
	@media (max-width: 900px) {
		.results {
			/* grid-template-columns: repeat(4, 1fr); */
		}
	}
	@media (max-width: 700px) {
		.results {
			/* grid-template-columns: repeat(3, 1fr); */
		}
	}
	.match {
		display: block;
		text-align: center;
		font-weight: bold;
	}
	.result {
		display: grid;
		grid-template-columns: auto 1fr 80px 2fr;
		column-gap: 5px;
		align-items: center;
		background: #88bcd2;
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
	.name {
		text-align: left;
	}
	.bar-container {
		position: relative;
		background: none;
		width: 100%;
		height: 8px;
	}
	.bar {
		height: 100%;
		position: absolute;
		left: 0;
		top: 0;
		background-color: #fff;
		border-radius: 2px;
	}
	.plus svg path {
		fill: #fff;
	}
</style>
