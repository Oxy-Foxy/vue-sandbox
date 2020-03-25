<template>
	<div class="product">
		<div class="product-image">
			<img v-bind:src="image" />
			<!-- <img v-bind:src="image2" /> -->
		</div>
		<div class="product-info">
			<h1>{{ title }}</h1>
			<p>{{ description }}</p>

			<p v-if="inventory > 10">In Stock</p>
			<p v-else-if="inventory <= 10 && inventory > 0">
				Almost Out of Stock
			</p>
			<p v-else :style="{ 'text-decoration': 'line-through' }">
				Out of Stock
			</p>
			<p v-show="onSale">On Sale</p>

			<p>Shipping: {{ shipping }}</p>

			<product-details :details="details"></product-details>

			<div
				v-for="(variant, index) in variants"
				:key="variant.id"
				class="color-box"
				:style="{ backgroundColor: variant.value }"
				@mouseover="updateProduct(index)"
			></div>
			<div class="d-flex">
				<div v-for="size in sizes" :key="size.id" class="d-flex">
					<label
						class="d-flex ais"
						:class="[
							{
								disabled:
									variants[selectedImage].inventory[
										size.id
									] == 0
							},
							{ checked: size.checked }
						]"
					>
						<input
							type="radio"
							name="sizes"
							class="visually-hidden"
							:id="size.id"
							@change="setSizeSelected(size.id, $event)"
						/>
						<div class="d-flex f-d-col">
							<span>size: {{ size.value }}</span>
							<span
								>in stock:
								{{
									variants[selectedImage].inventory[size.id]
								}}</span
							>
						</div>
					</label>
				</div>
			</div>
			<div class="d-flex">
				<button
					v-on:click="addToCart"
					:disabled="available <= 0"
					:class="{ disabledButton: inventory <= 0 }"
				>
					Add to Cart
				</button>
				<!-- <button v-on:click="removeFromCart">Remove From Cart</button> -->
			</div>
			<div class="cart">
				<p>Cart {{ cart }}</p>
			</div>
		</div>
	</div>
</template>
<script>
	import productDetails from './product-details';
	import greenSocks from '@/assets/vmSocks-green-onWhite.jpg';

	export default {
		name: 'product',
		props: {
			premium: {
				type: Boolean,
				required: true
			}
		},
		components: { productDetails },
		data() {
			return {
				brand: 'Vue Mastery',
				product: 'Socks',
				description: 'A pair of warm, fuzzy socks',
				selectedImage: 0,
				selectedSize: null,
				available: 100,
				cart: 0,
				details: [
					{ value: '80% cotton', id: 'd1' },
					{ value: '20% polyester', id: 'd2' },
					{ value: 'Gender neutral', id: 'd3' }
				],
				variants: [
					{
						value: 'green',
						id: 'v1',
						image: greenSocks,
						inventory: { s1: 3, s2: 4, s3: 0, s4: 3 },
						onSale: true
					},
					{
						value: 'blue',
						id: 'v2',
						image: 'images/vmSocks-blue-onWhite.jpg',
						inventory: { s1: 10, s2: 0, s3: 20, s4: 20 },
						onSale: false
					}
				],
				sizes: [
					{ value: '36', id: 's1', checked: null },
					{ value: '38', id: 's2', checked: null },
					{ value: '40', id: 's3', checked: null },
					{ value: '42', id: 's4', checked: null }
				],
				selectedItems: [],
				link:
					'https://www.vuemastery.com/courses/intro-to-vue-js/attribute-binding',
				children: '' // without this property - warning in console
			};
		},
		mounted() {
			console.log(this);
		},
		methods: {
			addToCart() {
				this.variants[this.selectedImage].inventory[
					this.selectedSize
				] -= 1;
				// if (this.cart >= this.available) return;
				this.cart += 1;
			},
			// removeFromCart() {
			//   if (this.cart <= 0) return;
			//   this.cart -= 1;
			// },
			updateProduct(index) {
				this.selectedImage = index;
			},
			setSizeSelected(id) {
				this.sizes.map(size => {
					return (size.checked = size.id == id ? true : null);
				});
				this.selectedSize = id;
			}
		},
		computed: {
			title() {
				return this.brand + ' ' + this.product;
			},
			image() {
				return this.variants[this.selectedImage].image;
			},
			inventory() {
				return Object.values(
					this.variants[this.selectedImage].inventory
				).reduce((acc, currVal) => acc + currVal);
			},
			onSale() {
				return this.variants[this.selectedImage].onSale;
			},
			shipping() {
				if (this.premium) {
					return 'Free';
				} else {
					return '2.99';
				}
			}
		}
	};
</script>
