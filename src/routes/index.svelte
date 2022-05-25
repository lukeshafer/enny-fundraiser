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

<main class:activate={activateMain}>
	<h1>Enny's Wheels</h1>

	<h2><strong>Help Enny get a wheelchair!</strong></h2>

	<ul>
		<li>
			<a class="btn main" href="https://chuffed.org/project/ennys-wheels" title="Donate">Donate!</a>
		</li>
	</ul>

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
		You can donate on Chuffed by clicking the above button, or on Venmo or Paypal via the below
		links, if you prefer. <strong
			>If you use Venmo, please be sure to include a note that it's for Enny!</strong
		>
	</p>

	<ul>
		<li>
			<a
				class="btn"
				href="https://account.venmo.com/pay?recipients=anahitacreates&note=For%20Enny!"
				title="AnahitaCreates Venmo">Venmo</a
			>
		</li>
		<li>
			<a
				class="btn"
				href="https://www.paypal.com/donate/?business=XKHZ8DD8P9X5J&no_recurring=1&item_name=To+support+Enny+and+purchase+them+a+wheelchair%21&currency_code=USD"
				title="AnahitaCreates Paypal">Paypal</a
			>
		</li>
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
