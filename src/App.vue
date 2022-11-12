<template>
  <div id="app">
    <div class="nav-bar"></div>
    <div class="cart">Cart({{ cart.length }})</div>
    <ProductDisplay :premium="premium" @add-to-cart="updateCart"></ProductDisplay>
  </div>
</template>

<script>
import ProductDisplay from "./components/product-display.vue";

export default {
  name: "App",
  data() {
    return {
      cart: [],
      premium: true,
    };
  },
  components: {
    ProductDisplay,
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    }
  }
};
</script>

<style>
</style>
