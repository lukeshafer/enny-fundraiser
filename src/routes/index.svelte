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
	let linkSection: HTMLElement;
	let footerTop = 0;
	let floatOpacity = 0.3;

	onMount(() => {
		if (linkSection) footerTop = linkSection.offsetTop;
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
	<meta name="theme-color" content="#c7e9fa" />
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
			<iframe
				class="float"
				title="Chuffed Preview"
				width="100%"
				height="340"
				src="https://chuffed.org/iframe/91190/25aae1"
				frameborder="0"
				allowfullscreen
				on:mouseenter={() => (floatOpacity = 1)}
				on:mouseleave={() => (floatOpacity = 0.3)}
				style:opacity="min({(footerTop - (y + windowHeight)) / 100}, {floatOpacity})"
				style="max-width:310px;border:0px solid #fff;margin:0 auto;"
			/>
			<!-- <a
				class="float-btn btn float"
				href="https://chuffed.org/project/ennys-wheels"
				style:opacity={(footerTop - (y + windowHeight)) / 100}>Donate!</a
			> -->
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
	<h2>How you can support!</h2>
	<p>
		Click the <strong>Donate</strong> button below to visit the Chuffed.org campaign and donate
		directly! Alternatively, if you prefer to use Paypal or Venmo, follow the links below to donate!
		<em
			>If you pay with Venmo, please make sure to leave a note mentioning the donation is for Enny!</em
		>
	</p>
</main>

<section id="link-section" bind:this={linkSection}>
	<div class="btn-container btn-footer">
		<a class="btn" href="https://chuffed.org/project/ennys-wheels">Donate directly!</a>
	</div>
	<a class="zine" href="https://www.anahitacreates.com/product/fundraiser-better-place-zine"
		><p>Purchase a <em>Better Place Zine</em> from AnahitaCreates!</p>
	</a>
	<div class="link-container">
		<a
			id="venmo"
			class="alt-payment-link"
			href="https://account.venmo.com/pay?recipients=anahitacreates&note=For%20Enny!"
			title="AnahitaCreates Venmo"
			target="_blank"
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
</section>

<footer><h2>Thank you for your support! ♥️</h2></footer>
