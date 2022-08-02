<script>

	import { onMount } from 'svelte'

	export let key = ''

	let errorMessage = ''
	let token = ''
	// 
	// パブリックキーを入力しないとエラーになるよ
	// 
	let payjp = Payjp(key)

	let elements = payjp.elements()

	let cardElement = elements.create('card')

	function init() {
		cardElement.mount('#v2-demo')
	}

	function click() {
		console.log('post')
		payjp.createToken(cardElement).then((r) => {
			if (r.error) {
				errorMessage = r.error.message
			} else {
				token = r.id
				console.log(r)
			}
		})
	}

	onMount(() => {
		init()
	})
</script>

<form>
	<div id="v2-demo" class="payjs-outer"><!-- ここにフォームが生成されます --></div>
	<button on:click|preventDefault={ click }>トークン作成</button>

	<span id="token">{ token }</span>
	{ #if errorMessage }
		<div>{ errorMessage }</div>
	{ /if }
</form>