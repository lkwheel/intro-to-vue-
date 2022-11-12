<template>
  <div id="app">
    <div class="nav-bar"></div>

    <div class="cart">Cart({{ cart }})</div>

    <div class="product-display">
      <div class="product-container">
        <div
          class="product-image"
          :class="{ 'out-of-stock-img': !(inventory > 0) }"
        >
          <BaseImage :src="src" :alt="alt" />
        </div>
        <div class="product-info">
          <h1>{{ title }}</h1>
          <p v-if="inventory > 10">In stock</p>
          <p v-else-if="inventory <= 10 && inventory > 0">
            Almost out of stock
          </p>
          <p v-else>Out of stock</p>
          <ul>
            <li v-for="(detail, index) in details" :value="index" :key="detail">
              {{ detail }}
            </li>
          </ul>
          <div
            v-for="variant in variants"
            :key="variant.id"
            class="color-circle"
            :class="[variant.image === src ? activeClass : '']"
            :style="{ backgroundColor: variant.color }"
            @mouseover="updateImage(variant)"
          ></div>
          <button
            class="button"
            :class="{ disabledButton: !(inventory > 0) }"
            :disabled="!(inventory > 0)"
            @click="addToCart"
          >
            Add to Cart
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const greenSocks = "socks_green.jpg";
const greenSocksAlt = "Green Socks";
const blueSocks = "socks_blue.jpg";
const blueSocksAlt = "Blue Socks";
import BaseImage from "./components/BaseImage";
export default {
  name: "App",
  components: {
    BaseImage,
  },
  data: () => {
    return {
      activeClass: 'active-circle',
      cart: 0,
      product: "Socks",
      brand: "Vue Mastery",
      inventory: 10,
      details: ["50% cotton", "30% wool", "20% ployester"],
      src: blueSocks,
      alt: blueSocksAlt,
      variants: [
        { id: 2234, color: "green", image: greenSocks, alt: greenSocksAlt, quantity: 50 },
        { id: 2235, color: "blue", image: blueSocks, alt: blueSocksAlt, quantity: 0 },
      ],
    };
  },
  computed: {
    // inStock() {
    //   return this.inventory > 0;
    // }
    title() {
      return this.brand + " " + this.product;
    },
  },
  methods: {
    // Note: don't use arrow functions on instance properties
    // See: https://v2.vuejs.org/v2/guide/instance.html#Properties-and-Methods
    addToCart() {
      this.cart = ++this.cart;
    },
    updateImage(variant) {
      this.src = variant.image;
      this.alt = variant.alt;
    },
  },
};
</script>

<style>
</style>
