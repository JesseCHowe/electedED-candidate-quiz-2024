<script>
	export let index;
	export let total;
</script>

<section>
	<div class="container">
		<span>Question {index} of {+total}</span>
		<div class="bar">
			<span class="progress" style="width: {(+index / +total) * 100}%" />
		</div>
		<!-- <div class="categories">
			<span>Education</span>
			<span>Environment</span>
			<span>Crime and Safety</span>
			<span>Civic Engagement</span>
			<span>Civil Rights</span>
			<span>Economic Justice</span>
			<span>Human Needs</span>
			<span>Immigration</span>
			<span>Human Trafficking</span>
		</div> -->
	</div>
</section>

<style>
	* {
		color: #fff;
	}
	section {
		position: absolute;
		width: 100%;
		height: 20px;
	}
	.container {
		height: 10px;
		padding: 0 20px;
		max-width: 600px;
		margin: 0 auto;
		position: relative;
	}
	.bar {
		width: 100%;
		height: 10px;
		background-color: #fff;
		position: relative;
	}
	.progress {
		position: absolute;
		top: 0;
		left: 0;
		height: 100%;
		background-color: #c7871e;
		transition: 0.5s;
	}
</style>
