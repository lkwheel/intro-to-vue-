<template>
  <div id="app">
    <AppHeader></AppHeader>
    <div class="cart">Cart({{ cart.length }})</div>
    <ProductDisplay
      :premium="premium"
      @add-to-cart="updateCart"
    ></ProductDisplay>
  </div>
</template>

<script>
import AppHeader from '@/components/app-header.vue';
import ProductDisplay from './components/product-display.vue';

export default {
  name: 'App',
  data() {
    return {
      cart: [],
      premium: true,
    };
  },
  components: {
    AppHeader,
    ProductDisplay,
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
};
</script>

<style>
</style>
