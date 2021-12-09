<script>
	import  Entry from '../components/entry.svelte'
	import { onMount } from 'svelte';
	const url = "https://gkapi.thomasorus.com"
	// const url = "https://localhost:3001/"

	let data = undefined

	onMount(async () => {
		const res = await fetch(url);
		data = await res.json();
	});

</script>

	{#if data === undefined}
	       <h2> Loading Data...</h2>
	{:else}

	    {#each data.entries as entr}
	    	<Entry data={entr}/>
	    {/each}
	{/if}

<style global>


	a {
		text-decoration: underline;
	}
	p {
		font-size: 1rem;
		line-height: 1.5;
	}
</style>