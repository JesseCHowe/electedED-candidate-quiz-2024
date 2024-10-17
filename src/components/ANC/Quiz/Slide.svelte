<script>
	export let question;
	export let selAnswer;
	export let activeSlide;

	const selectAnswer = (answer) => {
		question.answer = answer;
		activeSlide++;
	};
</script>

<section>
	<div class="container">
		<div class="top">
			<div class="bg" />
			<div class="inner">
				<span class="category">{question.Category}</span>
				<p>
					{@html question.Text}
				</p>
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
			class="wave"
			preserveAspectRatio="xMidYMid meet"
		>
			<path
				d="M0.1,119.43V67.45c0,0,99.87,71.51,322.45,8.12c5.56-1.66,92.01-26.52,125.74-35.72
	c77.28-21.08,219.28-41.4,311.28-38.34c233,7.77,323.98,82.1,469.23,96.61c149.64,14.94,288.45-12.46,371.26-36.99v55.34L0.1,119.43
	z"
			/>
		</svg>
		<div class="bottom">
			<div class="btns">
				<button on:click={() => selectAnswer("yes")}>
					<span>Yes</span>
				</button>
				<button on:click={() => selectAnswer("no")}>
					<span>No</span>
				</button>
				<button on:click={() => selectAnswer("no answer")}>
					<span>Skip</span>
				</button>
			</div>
		</div>
	</div>
</section>

<style>
	* {
		font-family: sans-serif;
	}
	path {
		fill: #88bcd2;
	}
	.category {
		background: #fff;
		border-radius: 5px;
		color: #000;
		font-weight: bold;
		font-size: 13px;
		padding: 5px;
	}
	.container {
		height: calc(100vh - 90px);
		display: grid;
		grid-template-rows: 1fr auto 1fr;
	}
	.top {
		padding-top: 40px;
		position: relative;
	}
	.top .inner {
		max-width: 600px;
		margin: 30px auto;
		padding: 0 20px;
	}

	.bottom {
		background: #88bcd2;
		padding: 0 20px;
		display: flex;
		align-items: center;
		z-index: 100;
	}
	p {
		font-size: 24px;
		line-height: 1.5;
		color: #fff;
		text-shadow: 2px 2px rgba(0, 0, 0, 0.2);
		opacity: 1;
	}
	* {
		color: #efefef;
	}
	.btns {
		display: grid;
		grid-template-columns: 1fr;
		row-gap: 15px;
		width: 100%;
		max-width: 600px;
		margin: 0 auto;
	}
	button {
		display: block;
		width: 100%;
		color: #000;
		background-color: #efefef;
		position: relative;
		padding: 20px;
		border-radius: 10px;
	}
	button:hover {
		background-color: #255970;
	}
	button:hover span {
		color: #fff;
	}
	button span {
		font-size: 20px;
		font-weight: bold;
		color: #000;
	}
	.wave {
		z-index: 100;
		position: relative;
	}
</style>
