<script>
	export let activeSlide, copy;
</script>

<section>
	<div class="container">
		<div class="top">
			<h1>{copy.Title}</h1>
			<span class="published">04/19/2024</span>
			<p>{copy.Desc}</p>
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
	.btn-content {
		display: flex;
		justify-content: space-between;
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
		grid-template-rows: 2fr auto 1fr;
	}
	.top {
		padding: 0 20px 40px;
		max-width: 600px;
		margin: 0 auto;
	}
	.bottom {
		background: #c7871e;
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
		line-height: 1;
		margin: 0;
		font-size: 75px;
		color: #efefef;
		font-weight: bold;
	}
	p {
		font-size: 20px;
		line-height: 1.5;
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
	}
	path {
		fill: #c7871e;
	}
</style>
