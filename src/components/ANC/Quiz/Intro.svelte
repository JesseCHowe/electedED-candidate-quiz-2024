<script>
	export let activeSlide, copy, ward;
</script>

<section>
	<div class="container">
		<div class="top">
			<div class="wards">
				<button class={ward === 7 ? "active" : ""} on:click={() => (ward = 7)}
					>Ward 7 quiz</button
				>
				<button class={ward === 8 ? "active" : ""} on:click={() => (ward = 8)}
					>Ward 8 quiz</button
				>
			</div>
			<h1>Find your Ward {ward} Advisory Neighborhood Commissioner match</h1>
			<p>
				Compare your stances on issues impacting education, environment, crime
				and safety, and economic justice with those of the candidates running
				for the Council of the District of Columbia to represent Ward {ward}.
			</p>
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
		<div class="bottom">
			<div class="inner">
				<button on:click={() => activeSlide++}>
					<div class="btn-content">
						<span>Begin</span>
						<div class="arrow">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								width="20px"
								height="20px"
								viewBox="0 0 24 24"
								{...$$props}
								><path
									fill="currentColor"
									d="M8.025 22L6.25 20.225L14.475 12L6.25 3.775L8.025 2l10 10z"
								/></svg
							>
						</div>
					</div>
				</button>
			</div>
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
	.btn-content {
		display: flex;
		justify-content: space-between;
	}
	button {
		margin: 0 auto;
	}
	button span {
		font-weight: bold;
		font-size: 20px;
	}
	@keyframes example {
		0% {
			transform: translate(0);
		}
		50% {
			transform: translate(-100%);
		}
		100% {
			transform: translate(0);
		}
	}

	.arrow {
		animation-name: example;
		animation-duration: 2s;
		animation-iteration-count: infinite;
	}

	.container {
		height: calc(100vh - 90px);
		display: grid;
		grid-template-rows: 1.5fr auto 1fr;
	}
	.top {
		padding: 0 20px 40px;
		max-width: 600px;
		margin: 0 auto;
	}
	.bottom {
		background: #88bcd2;
		z-index: 100;
		display: flex;
		/* justify-content: center; */
		align-items: flex-start;
	}
	.inner {
		width: 100%;
		max-width: 600px;
		margin: 0 auto;
		padding: 20px;
	}
	* {
		color: #efefef;
	}
	h1 {
		font-family: sans-serif;
		line-height: 1.2;
		margin: 0;
		font-size: 40px;
		color: #efefef;
		font-weight: bold;
		text-align: center;
	}
	p {
		font-size: 20px;
		line-height: 1.5;
		text-align: center;
	}
	button {
		background: #fff;
		color: #000;
		width: 100%;
		max-width: 250px;
		display: block;
		padding: 20px;
		border-radius: 15px;
		text-align: left;
	}
	button span {
		color: #000;
	}
	#curved-border {
		/* bottom: 0; */
		/* position: absolute; */
		z-index: 100;
	}
	path {
		fill: #88bcd2;
	}
</style>
