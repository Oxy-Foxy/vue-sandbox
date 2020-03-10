<template>
  <div id="app">
    <div class="product">
      <div class="product-image">
        <img v-bind:src="image" />
        <!-- <img v-bind:src="image2" /> -->

        <a :href="link">Attribute Binding</a>
      </div>
      <div class="product-info">
        <h1>{{product}}</h1>
        <p>{{description}}</p>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost Out of Stock</p>
        <p v-else>Out of Stock</p>
        <p v-show="onSale">On Sale</p>
        <ul>
          <li v-for="detail in details" :key="detail.id">{{detail.value}}</li>
        </ul>
        <div v-for="variant in variants" :key="variant.id">
          <p @mouseover="updateProduct(variant.image)">{{variant.value}}</p>
        </div>
        <div class="d-flex">
          <div v-for="size in sizes" :key="size.id">{{size.value}}</div>
        </div>
        <div class="d-flex">
          <button v-on:click="addToCart">Add to Cart</button>
          <button v-on:click="removeFromCart">Remove From Cart</button>
        </div>
        <div class="cart">
          <p>Cart {{cart}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import greenSocks from "@/assets/vmSocks-green-onWhite.jpg";

export default {
  name: "App",
  data() {
    return {
      product: "Socks",
      description: "A pair of warm, fuzzy socks",
      image: greenSocks,
      image2: "images/vmSocks-blue-onWhite.jpg",
      available: 100,
      inventory: 10,
      onSale: false,
      cart: 0,
      details: [
        { value: "80% cotton", id: "d1" },
        { value: "20% polyester", id: "d2" },
        { value: "Gender neutral", id: "d3" }
      ],
      variants: [
        { value: "green", id: "v1", image: greenSocks },
        { value: "blue", id: "v2", image: "images/vmSocks-blue-onWhite.jpg" }
      ],
      sizes: [
        { value: "36", id: "s1" },
        { value: "38", id: "s2" },
        { value: "40", id: "s3" },
        { value: "42", id: "s4" }
      ],
      link:
        "https://www.vuemastery.com/courses/intro-to-vue-js/attribute-binding",
      children: "" // without this property - warning in console
    };
  },
  mounted() {
    console.log(this);
  },
  methods: {
    addToCart() {
      if (this.cart >= this.available) return;
      this.cart += 1;
    },
    removeFromCart() {
      if (this.cart <= 0) return;
      this.cart -= 1;
    },
    updateProduct(src) {
      this.image = src;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.d-flex {
  display: flex;
}

.d-flex > * + * {
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
}

.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px;
  border: 1px solid #d8d8d8;
}

input {
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
