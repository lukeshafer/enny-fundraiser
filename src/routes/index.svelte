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

	let y: number;
	let windowHeight: number;
	let footer: HTMLElement;
	let footerTop = 0;

	onMount(() => {
		if (footer) footerTop = footer.offsetTop;
	});

	const scrollToTop = () => {
		document.body.scrollTop = 0; // For Safari
		document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
	};
</script>

<svelte:window bind:scrollY={y} bind:innerHeight={windowHeight} />

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
		<img id="burst" src="/assets/burst-frame.svg" width="0" alt="" />
	</div>
	<ul id="chairs">
		{#each wheelChairs as index}
			<img
				id="chair{index}"
				class="chair"
				src="assets/wheelchair.svg"
				width="0"
				alt=""
				style:left="{xs[index]}vw"
				style:top="{ys[index]}vh"
				style:transform="rotate({random(40) - 10}deg) scaleX({Math.pow(-1, random(2))})"
			/>
		{/each}
	</ul>
</div>

<div class="header-wrapper">
	<header class:activate={activateMain}>
		<h1 style:--opacity={0.3 + 100 / y} on:click={scrollToTop} class:scrollToTop={y > 500}>
			Enny's Wheels
		</h1>
		<img id="enny" src="assets/enny.png" width="400" alt="Enny" style:opacity={1 - y / 300} />
		<div class="cloud-container">
			<img
				id="cloud-left"
				class="cloud"
				src="assets/cloud.svg"
				alt=""
				width="0"
				style:transform="translateX({y}px)"
				style:opacity={2 - y / 300}
			/>
		</div>
		<div class="cloud-container">
			<img
				id="cloud-right"
				class="cloud"
				src="assets/cloud.svg"
				alt=""
				width="0"
				style:transform="scaleX(-1) translateX({y}px)"
				style:opacity={2 - y / 300}
			/>
		</div>
		<div class="btn-container">
			<a
				class="float-btn btn"
				href="https://chuffed.org/project/ennys-wheels"
				style:opacity={(footerTop - (y + windowHeight)) / 100}>Donate!</a
			>
		</div>
	</header>
</div>

<main style:opacity={y / 300 - windowHeight / 900}>
	<h2>Help Enny get a wheelchair!</h2>
	<p>
		Enny is disabled and currently waiting to be put on the transplant list for a new liver,
		hopefully by July. Enny is also Black, trans, and queer, and with Pride Month coming up, it's
		important to keep in mind that the first Pride was a riot started by trans people of color.
		<strong>Please consider donating especially if you're a person with privilege</strong>.
	</p>

	<p>
		<strong>Enny loves crocheting, painting, gaming, and many other creative hobbies.</strong>
		Having a wheelchair will help him get to medical appointments, pick up their medication, check their
		mail, and get around safely and stress-free. They live in a place with grass and dangerous sidewalks,
		so
		<strong>
			we're hoping to fundraise $2,500 for a motorized wheelchair capable of navigating multiple
			terrains
		</strong>.
	</p>

	<p>
		Click the <strong>Donate</strong> button below to visit the Chuffed.org campaign for Enny's
		wheelchair. Alternatively, if you prefer to use Paypal or Venmo, follow the links below to
		donate!
		<em
			>If you pay with Venmo, please make sure to leave a note mentioning the donation is for Enny!</em
		>
	</p>
</main>

<footer bind:this={footer}>
	<div class="btn-container btn-footer">
		<a class="btn" href="https://chuffed.org/project/ennys-wheels">Donate!</a>
	</div>
	<div class="link-container">
		<a
			id="venmo"
			class="alt-payment-link"
			href="https://account.venmo.com/pay?recipients=anahitacreates&note=For%20Enny!"
			title="AnahitaCreates Venmo"
			><img src="/assets/venmo_logo_blue.svg" width="240" alt="Donate with Venmo" /></a
		>
		<a
			id="paypal"
			class="alt-payment-link"
			href="https://www.paypal.com/donate/?business=XKHZ8DD8P9X5J&no_recurring=1&item_name=To+support+Enny+and+purchase+them+a+wheelchair%21&currency_code=USD"
			title="AnahitaCreates Paypal"
			><img src="/assets/pp-logo-200px.png" width="240" alt="Donate with PayPal" /></a
		>
	</div>
</footer>

<style>
	header {
		visibility: hidden;
	}

	header.activate {
		visibility: visible;
	}

	#background-layout,
	#background-layout * {
		z-index: -1;
	}

	.header-wrapper {
		height: 100vh;
		display: flex;
		align-items: center;
	}

	#background-layout {
		background: url('/assets/background.png');
		background-size: cover;
		position: fixed;
		width: 100%;
		height: 100%;
	}

	.chair {
		width: 6em;
		position: absolute;
	}

	#burst-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100%;
	}

	#burst {
		height: 90vh;
	}

	#enny {
		height: calc(100% + 2em);
		width: calc(100% + 2em);
		grid-row: 2;
		grid-column: 2 / 3;
		object-fit: contain;
	}

	.cloud {
		position: absolute;
		object-fit: contain;
		width: 50em;
	}

	.cloud-container {
		position: relative;
		grid-column: 2;
		grid-row: 2;
	}

	#cloud-left {
		bottom: -10em;
		right: -2em;
	}

	#cloud-right {
		bottom: -10em;
		left: -2em;
	}

	strong {
		--outline: var(--strong);
		font-weight: 900;
		color: var(--dark-second);
		text-shadow: 0 0 5px var(--outline);
		letter-spacing: 1px;
	}

	a {
		text-decoration: none;
	}

	.btn-container {
		/* grid-column: 1/3; */
		z-index: 1;
		/* justify-self: left; */
		display: flex;
		flex-flow: column;
		align-items: center;
	}

	.btn::before {
		align-self: center;
		background: #00000000 url('/assets/hand-heart.svg') no-repeat center;
		background-size: contain;
		display: block;
		width: 100%;
		height: 2em;
		content: '';
	}

	.btn {
		color: var(--btn-text);
		background: #00000077;
		padding: 0.3em;
		font: var(--subheading);
		font-size: 3em;
		white-space: nowrap;
	}

	.btn:hover {
		font-size: 3.2em;
		filter: brightness(120%);
	}

	.float-btn {
		position: fixed;
		bottom: 1em;
		right: 1em;
	}

	.float-btn:hover {
		font-size: 3.7em;
		filter: brightness(120%);
	}

	.link-container {
		display: grid;
		width: 100%;
		grid-template-columns: repeat(auto-fit, minmax(12em, 1fr));
		grid-auto-rows: 4em;
		place-items: center;
		gap: 2em;
		/* justify-content: center;
		flex-flow: row wrap; */
	}

	.alt-payment-link {
		display: block;
		height: 2em;
		width: auto;
		background: white;
		padding: 1em;
	}

	.alt-payment-link:hover {
		padding: 1.2em;
		filter: brightness(120%);
	}

	.alt-payment-link > img {
		height: 2em;
		width: 8em;
		object-fit: cover;
	}

	h1 {
		opacity: var(--opacity);
	}

	h1.scrollToTop:hover {
		cursor: pointer;
		opacity: 1;
	}

	@media (prefers-reduced-motion: reduce) {
		header.activate > h1 {
			animation: none;
		}
		header.activate img#cloud-left {
			animation: none;
		}

		header.activate img#cloud-right {
			animation: none;
		}

		.btn {
			transition: none;
		}

		#venmo,
		#paypal {
			transition: none;
		}
	}

	@media (prefers-reduced-motion: no-preference) {
		header.activate > h1 {
			animation: fade-in 800ms ease-out;
		}

		h1 {
			transition: opacity 300ms;
		}

		header.activate img.cloud {
			--delay: 500ms;
			transition: visibility 800ms var(--delay);
		}
		header.activate img#cloud-left {
			animation: slide-in-left 800ms ease-out var(--delay);
		}

		header.activate img#cloud-right {
			animation: slide-in-right 800ms ease-out var(--delay);
		}

		header.activate img#enny {
			transition: visibility 800ms 601ms;
			animation: slide-in-bottom 800ms ease-out 600ms;
		}

		.btn {
			transition: font-size 200ms cubic-bezier(0.57, -1, 0.41, 2);
		}

		#venmo,
		#paypal {
			transition: padding 200ms cubic-bezier(0.57, -1, 0.41, 2);
		}
	}
</style>
