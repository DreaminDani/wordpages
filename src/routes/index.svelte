<script>
	let rendered = false;
	let words = '';
	let wordList = [''];

	function renderWords() {
		wordList = words.split('\n');
		console.log(wordList);
		rendered = true;
	}
</script>

<svelte:head><title>Word Pages</title></svelte:head>

{#if rendered}
	{#each wordList as word, i}
		{#if (i + 1) % 4 === 0}
			<span>{word}</span>
			<br />
		{:else}
			<span>{word}</span>
		{/if}
		{#if (i + 1) % 20 === 0}
			<div class="pagebreak" />
		{/if}
	{/each}
{:else}
	<h1>Word Pages</h1>
	<p>Make a bunch of pages with words on them (20 words per page)</p>
	<small>Enter a list of words with a newline between each word...</small>
	<br />
	<textarea bind:value={words} name="words" cols="20" rows="20" />
	<br />
	<button on:click={renderWords}>Submit</button>
{/if}

<style>
	span {
		display: inline-block;
		font-size: 40px;
		margin-right: 20px;
		margin-top: 20px;
	}

	@media print {
		.pagebreak {
			page-break-before: always;
		}
	}
</style>
