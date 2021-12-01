<script>
	import { onMount } from 'svelte';
	const url = "https://gkapi.thomasorus.com"
	let data

	onMount(async () => {
		const res = await fetch(url);
		data = await res.json();
		// data.sort(function(a,b){
		//   return new Date(b.pubDate) - new Date(a.pubDate);
		// });
	});

	function loadContent (el) {
		console.log(el)
	}
</script>

<article class="flow-2">
	{#if data === undefined}
	       <h2> Loading Data...</h2>
	{:else}
		<ul class="flow-2">
	    {#each data.entries as entr}
	    	<li class="flow-1">
	    		<img src={entr.image} alt={entr.title}>
	    		<h2>{entr.title}</h2>
	    		<span>Par : {entr.creator}</span> le <time>{entr.pubDate}</time>
	    		<p>{entr.description}</p>
	    		<button on:click={loadContent}>Charger l'article</button>
	    		<a href={entr.link}>Voir sur GK</a>
	    	</li>

	    {/each}
	    </ul>
	{/if}
</article>

<style>
	article {
		max-width: 100ch;
		margin: auto;
		padding: 2em;
	}
	li {
		position: relative;
	}
	img {
		max-width: 100%;
	}
	.absolute-link {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.flow-1 > *+* {
		margin-top: 1em;
	}
	.flow-2 > *+* {
		margin-top: 2em;
	}
	button {
		background-color: #191919;
		color: white;
		padding: 0.5em;
		border: none;
		border-radius: 1em;
	}
	a {
		text-decoration: underline;
	}
	p {
		font-size: 1rem;
		line-height: 1.5;
	}
</style>