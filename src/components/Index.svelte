<script>
	import Slide from "./Quiz/Slide.svelte";
	import Intro from "./Quiz/Intro.svelte";
	import Answers from "./Quiz/Answers.svelte";
	import Progress from "./Quiz/Progress.svelte";
	import copy from "$data/copy.json";
	$: questions = copy.questions.map((d) => {
		return {
			...d,
			answer: undefined
		};
	});
	let activeSlide = 0;
</script>

<section>
	{#if activeSlide === 0}
		<Intro bind:activeSlide {copy} />
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
		<Answers bind:activeSlide {questions} />
	{/if}
</section>

<style>
	section {
		/* padding: 10px; */
		margin: 0 auto;
		/* max-width: 600px; */
	}
</style>
