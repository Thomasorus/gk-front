<script>
	export let data;
	let entr = data
		const url = "https://gkapi.thomasorus.com/"

	async function loadContent (el) {
		const res = await fetch(`${url}fetchContent/${el}`);
		let entry = await res.json();

		if(entry.entry !== undefined) {
			entr.content = entry.entry[0].content
		} else {
			entr.content = "Cet article est résevé aux premiums. Abonnez-vous !"
		}
	}
</script>

<article>
	<img loading="lazy" src={entr.image} alt={entr.title}>
	<h2>{entr.title}</h2>
	<span>Par : {entr.creator}</span> le <time>{entr.pubDate}</time>
	<p>{entr.description}</p>
	<a href={entr.link}>Voir sur GK</a>
	 <details>
		  <summary on:click={loadContent(entr.id)}>Charger l'article</summary>
		  <div class="details">
		  	{@html entr.content}
		  </div>
	</details>
</article>

<style global>
	.details {
		padding: 1rem;
		border: 1px solid var(--c4);
	}
	article > *+*, details > *+* {
		margin-top: 1em;
	}
	article {
		max-width: 80ch;
		margin: auto;
		padding: 2em;
				margin-bottom: 1em;

	}

	summary {
		background-color: #191919;
		color: white;
		padding: 0.5em;
		border: none;
		border-radius: 1em;
		display: inline-block;
	}

	.details *+* {
		margin-top: 1em;
	}

</style>