<script>
	import { onMount } from 'svelte'

	export let key = ''

	let payForm

	let handler = Komoju.multipay.configure({
			key: key,
			token: function(token) {
				payForm.komojuToken.value = token.id
				payForm.submit()
			}
		})

	function click() {
		handler.open({
			amount:       1000,
			endpoint:     "https://komoju.com",
			locale:       "ja",
			currency:     "JPY",
			title:        "<商品名>",
			description:  "<商品説明>",
			methods: [
    			"credit_card","konbini","bank_transfer","pay_easy","web_money","bit_cash","net_cash","japan_mobile","paypay","linepay","merpay","rakutenpay","nanaco","dospara","steam_prepaid_card"
    		]
		})
	}

	onMount(() => {
		let query = new URLSearchParams(window.location.search)
		console.log(query.get('komojuToken')) // show komojuToken
	})

</script>


<form id="pay-form" bind:this={ payForm }>
	<input type="hidden" name="komojuToken"/>

	<button id="customButton" on:click|preventDefault={ click }>今すぐ支払い</button>
</form>
