<script>
	export let candidate, answers, questions;

	$: isMatch = (reader, candidate) => {
		if (reader && candidate) {
			return reader.toLowerCase() === candidate.toLowerCase();
		} else {
			return false;
		}
	};
</script>

<section>
	<h3>Compare by question</h3>
	<div class="results">
		<div class="hed">
			<span>Question</span>
			<span>Your<br />answer</span>
			<span>{candidate.last}'s<br />answer</span>
			<span />
		</div>
		{#each questions as question, i}
			<div class="row">
				<span>{@html question.Text}</span>
				<span
					class="answer {question.answer.toLowerCase().split(' ').join('-')}"
					>{question.answer}</span
				>
				<span class="answer {answers[i][candidate.last].toLowerCase()}"
					>{answers[i][candidate.last]}</span
				>
				{#if isMatch(question.answer, answers[i][candidate.last])}
					<span class="match">
						<span>Match</span>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="1em"
							height="1em"
							viewBox="0 0 32 32"
							{...$$props}
							><path
								fill="#fff"
								d="M16 2a14 14 0 1 0 14 14A14 14 0 0 0 16 2m-2 19.59l-5-5L10.59 15L14 18.41L21.41 11l1.596 1.586Z"
							/><path
								fill="none"
								d="m14 21.591l-5-5L10.591 15L14 18.409L21.41 11l1.595 1.585z"
							/></svg
						>
					</span>
				{/if}
			</div>
		{/each}
	</div>
</section>

<style>
	section {
		max-width: 800px;
		margin: 0 auto;
	}
	.hed {
		display: grid;
		grid-template-columns: 3fr 0.75fr 0.75fr 1fr;
		column-gap: 10px;
		align-items: flex-end;
		margin-bottom: 8px;
		font-size: 14px;
		position: sticky;
		top: 0;
		border-bottom: 3px solid #fff;
		background-color: #88bcd2;
		padding: 10px 0;
	}
	.hed span:first-child {
		text-align: left;
	}
	.hed span {
		text-align: center;
	}
	.row {
		display: grid;
		grid-template-columns: 3fr 0.75fr 0.75fr 1fr;
		column-gap: 10px;
		align-items: flex-start;
		border-bottom: 1px solid rgba(255, 255, 255, 0.25);
		padding-bottom: 20px;
		margin-bottom: 20px;
	}
	.answer {
		max-width: fit-content;
		padding: 5px;
		margin: 0 auto;
		display: block;
		text-transform: capitalize;
		border-radius: 5px;
		font-weight: bold;
		font-size: 13px;
		color: #fff;
	}
	.match {
		font-weight: bold;
		font-size: 13px;
	}
	.yes {
		background: #3a7e56;
	}
	.no {
		background: #aa4a4a;
	}
	.no-answer {
		background-color: #ccc;
		color: #000;
	}
</style>
