<script>
	import Slide from "./Quiz/Slide.svelte";
	import Intro from "./Quiz/Intro.svelte";
	import Answers from "./Quiz/Answers.svelte";
	import Progress from "./Quiz/Progress.svelte";
	import Form from "$components/Form.svelte";
	import copy from "$data/copy-anc.json";
	$: questions = copy.questions.map((d) => {
		return {
			...d,
			answer: undefined
		};
	});
	let activeSlide = 0;
	let ward = 7;
</script>

<div class="bg">
	<img src="../assets/bg-image.png" />
</div>
<section>
	{#if activeSlide === 0}
		<Intro bind:activeSlide {copy} bind:ward />
	{/if}
	{#if activeSlide > 0 && activeSlide <= questions.length}
		<Progress index={activeSlide} total={questions.length} />
	{/if}
	{#each questions as question, i}
		{#if i + 1 === +activeSlide}
			<Slide {question} bind:activeSlide />
		{/if}
	{/each}
	{#if activeSlide > questions.length}
		<Answers bind:activeSlide {questions} bind:ward />
	{/if}
</section>
<Form />

<style>
	.iframe-bg {
		background: #fff;
		width: 100%;
		display: flex;
		justify-content: center;
	}
	iframe {
		overflow: hidden;
		display: block;
		width: 100%;
		margin: 0 auto;
		height: 1900px;
		border: none;
	}
	section {
		/* padding: 10px; */
		margin: 0 auto;
		/* max-width: 600px; */
	}
	.bg {
		position: fixed;
		height: calc(100vh);
		background-repeat: no-repeat;
		width: 100%;
		top: 0px;
		left: 0;
		background-size: cover;
		background-blend-mode: overlay;
		background-position: center;
		opacity: 0.2;
		z-index: -5;
	}
	.bg img {
		object-position: top center;
		object-fit: cover;
		width: 100%;
		height: 100%;
	}
</style>
