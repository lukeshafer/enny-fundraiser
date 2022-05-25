<script lang="ts">
	import 'normalize.css';
	import { onMount } from 'svelte';
	import '../animations.css';
	import '../app.css';

	let activateMain = false;

	onMount(() => {
		activateMain = true;
	});

	const random = (end: number) => {
		return Math.floor(Math.random() * end);
	};

	let wheelChairs = [...Array(6).keys()];

	const xs = wheelChairs.slice().map((i) => {
		return Math.pow(i % 4, 1.2) + 10 * i + 35 * Math.floor(i / 3);
	});

	const ys = wheelChairs.slice().map((i, undefined, l) => {
		return 20 * ((7 - i) % 3) + 4 * i;
	});
</script>

<svelte:head>
	<title>Enny's Wheels!</title>
	<meta name="description" content="Funding a wheelchair for Enny" />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" />
	<link rel="apple-touch-icon" sizes="180x180" href="/favicon/apple-touch-icon.png" />
	<link rel="icon" type="image/png" sizes="32x32" href="/favicon/favicon-32x32.png" />
	<link rel="icon" type="image/png" sizes="16x16" href="/favicon/favicon-16x16.png" />
	<link rel="manifest" href="/favicon/site.webmanifest" />
	<link
		href="https://fonts.googleapis.com/css2?family=Libre+Franklin:wght@600;700;800&family=Mukta:wght@300;400;500&family=Noticia+Text:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div id="background-layout" aria-hidden="true">
	<div id="burst-wrapper">
		<img id="burst" src="/assets/burst-frame.svg" alt="" />
	</div>
	<ul id="chairs">
		{#each wheelChairs as index}
			<img
				id="chair{index}"
				class="chair"
				src="assets/wheelchair.svg"
				width="100"
				alt=""
				style:left="{xs[index]}vw"
				style:top="{ys[index]}vh"
				style:transform="rotate({random(40) - 10}deg)"
			/>
		{/each}
	</ul>
</div>

<main class:activate={activateMain}>
	<h1>Enny's Wheels</h1>
	<img id="enny" src="assets/enny.png" width="400" alt="Enny" />
	<img id="cloud-left" class="cloud" src="assets/cloud.svg" alt="cloud" />
	<img id="cloud-right" class="cloud" src="assets/cloud.svg" alt="cloud" />
</main>

<style>
	main {
		visibility: hidden;
	}

	main.activate {
		visibility: visible;
	}

	#background-layout,
	#background-layout * {
		z-index: -1;
	}

	#background-layout {
		background: url('/assets/background.png');
		background-size: cover;
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		top: 0;
		width: 100%;
		height: 100vh;
	}

	.chair {
		width: 6em;
		position: absolute;
	}

	#burst-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100vh;
	}

	#burst {
		display: block;
		position: relative;
		height: 90vh;
		margin: auto;
	}

	.cloud {
		position: absolute;
		bottom: -4em;
		--x-position: -14em;
		width: 33em;
	}

	#cloud-left {
		left: var(--x-position);
		/* transform: translateX(40vw); */
	}

	#cloud-right {
		right: var(--x-position);
		transform: scaleX(-1);
		/* transform: translateX(40vw); */
	}

	@media (prefers-reduced-motion: reduce) {
		main.activate > h1 {
			animation: none;
		}
		main.activate > img#cloud-left {
			animation: none;
		}

		main.activate > img#cloud-right {
			animation: none;
		}
	}

	@media (prefers-reduced-motion: no-preference) {
		main.activate > h1 {
			animation: fade-in 800ms ease-out;
		}

		main.activate > img.cloud {
			--delay: 500ms;
			transition: visibility 0ms var(--delay);
		}
		main.activate > img#cloud-left {
			animation: slide-in-left 800ms ease-out var(--delay);
		}

		main.activate > img#cloud-right {
			animation: slide-in-right 800ms ease-out var(--delay);
		}
	}
</style>
