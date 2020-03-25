<template>
	<div id="app">
		<product :premium="premium"></product>
	</div>
</template>

<script>
	import product from './product.vue';

	export default {
		name: 'App',
		components: { product },
		data() {
			return {
				premium: true
			};
		}
	};
</script>

<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
	}

	.visually-hidden {
		position: absolute;
		clip: rect(0 0 0 0);
		width: 1px;
		height: 1px;
		margin: -1px;
		overflow: hidden;
		padding: 0;
	}

	body {
		font-family: tahoma;
		color: #282828;
		margin: 0px;
	}

	.d-flex {
		display: flex;
	}

	.f-d-col {
		flex-direction: column;
	}

	.ais {
		align-items: flex-start;
	}

	.d-flex:not(.f-d-col) > * + * {
		margin-left: 10px;
	}

	.nav-bar {
		background: linear-gradient(-90deg, #84cf6a, #16c0b0);
		height: 60px;
		margin-bottom: 15px;
	}

	.product {
		display: flex;
		flex-flow: wrap;
		padding: 1rem;
	}

	img {
		border: 1px solid #d8d8d8;
		width: 70%;
		margin: 40px;
		box-shadow: 0px 0.5px 1px #d8d8d8;
	}

	.product-image {
		width: 80%;
	}

	.product-image,
	.product-info {
		margin-top: 10px;
		width: 50%;
	}

	.color-box {
		width: 40px;
		height: 40px;
		margin-top: 5px;
	}

	.cart {
		margin-right: 25px;
		float: right;
		border: 1px solid #d8d8d8;
		padding: 5px 20px;
	}

	button {
		margin-top: 30px;
		border: none;
		background-color: #1e95ea;
		color: white;
		height: 40px;
		width: 100px;
		font-size: 14px;
	}

	.disabledButton {
		background-color: #d8d8d8;
		pointer-events: none;
	}

	.disabled {
		color: #d8d8d8;
		pointer-events: none;
	}

	.checked {
		outline: 1px solid green;
	}

	.review-form {
		width: 400px;
		padding: 20px;
		margin: 40px;
		border: 1px solid #d8d8d8;
	}

	input:not([type='radio']) {
		width: 100%;
		height: 25px;
		margin-bottom: 20px;
	}

	textarea {
		width: 100%;
		height: 60px;
	}

	.tab {
		margin-left: 20px;
		cursor: pointer;
	}

	.activeTab {
		color: #16c0b0;
		text-decoration: underline;
	}
</style>
