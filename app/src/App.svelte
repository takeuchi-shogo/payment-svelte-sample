<script>
	import { onMount } from 'svelte'

	import config from './config'

	import Komoju from './Komoju.svelte';
	import Payjp from './Payjp.svelte'


	export let name;

	// $: {
	// 	console.log('komoju key', config.komojuKey)
	// }

	onMount (() => {
		// console.log('pay.jp key', config.payjpKey)
	})


</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>


	<Payjp key={ config.payjpKey }/>

	<Komoju key={ config.komojuKey }/>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>