<script>
	let words = '';
	let wordList = [''];
	let isRandom = false;

	function renderWords() {
		console.log(isRandom);
		if (isRandom) {
			wordList = words
				.split('\n')
				.map((value) => ({ value, sort: Math.random() }))
				.sort((a, b) => a.sort - b.sort)
				.map(({ value }) => value);
		} else {
			wordList = words.split('\n');
		}
		console.log(wordList);
	}
</script>

<svelte:head><title>Word Pages</title></svelte:head>

{#if wordList.length > 1}
	<div class="container">
		{#each wordList as word, i}
			{#if i < 4}
				<div class="word first">{word}</div>
			{:else if (i + 1) % 4 === 0}
				<div class="word">{word}</div>
			{:else}
				<div class="word">{word}</div>
			{/if}
		{/each}
	</div>
{:else}
	<h1>Word Pages</h1>
	<p>Make a bunch of pages with words on them (24 words per page)</p>
	<small>Enter a list of words with a newline between each word...</small>
	<br />
	<textarea bind:value={words} name="words" cols="20" rows="20" />
	<br />
	<input type="checkbox" name="isRandom" bind:checked={isRandom} />
	<label for="isRandom">Print words in random order</label><br />
	<p>After you click "Submit", print in landscape on a letter sized paper without any margins</p>
	<button on:click={renderWords}>Submit</button>
{/if}

<style>
	.container {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr 1fr;
	}
	.word {
		display: inline-block;
		font-size: 60px;
		margin-top: 64.5px;
	}
	.first {
		margin-top: 24px;
	}
</style>
