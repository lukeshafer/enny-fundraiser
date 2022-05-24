<script lang="ts">
	import 'normalize.css';
	import { onMount } from 'svelte';
	import '../animations.css';
	import '../app.css';

	let activateMain = false;

	onMount(() => {
		activateMain = true;
	});
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" />
	<link
		href="https://fonts.googleapis.com/css2?family=Libre+Franklin:wght@600;700;800&family=Mukta:wght@300;400;500&family=Noticia+Text:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main class:activate={activateMain}>
	<h1>Enny's Wheels</h1>

	<h2>Help Enny get a wheelchair!</h2>

	<p>
		Enny has been having a hard time getting around for quite some time and they're waiting to
		hopefully be put on a transplant list so their quality of life can get better. We are working to
		help them feel more free to move around and that's the kind of freedom a wheelchair allows.
	</p>

	<p>Please consider donating below:</p>

	<ul>
		<li><a class="btn" href="/" title="GoFundMe?">GoFundMe</a></li>
	</ul>
</main>

<style>
	main {
		visibility: hidden;
	}

	main.activate {
		visibility: visible;
	}

	@media (prefers-reduced-motion: reduce) {
		main.activate {
			animation: none;
		}
	}

	@media (prefers-reduced-motion: no-preference) {
		main.activate {
			animation: slide-in 500ms ease-in-out;
		}
	}
</style>
