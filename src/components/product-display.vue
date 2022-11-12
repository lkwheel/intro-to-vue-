<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image" :class="{ 'out-of-stock-img': inStock <= 0 }">
        <img :src="src" :alt="alt" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock > 10">In stock</p>
        <p v-else-if="inStock <= 10 && inStock">Almost out of stock</p>
        <p v-else>Out of stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ul>
          <li v-for="(detail, index) in details" :value="index" :key="detail">
            {{ detail }}
          </li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          class="color-circle"
          :class="[variant.image === src ? activeClass : '']"
          :style="{ backgroundColor: variant.color }"
          @mouseover="updateVariant(index)"
        ></div>
        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          @click="addToCart"
        >
          Add to Cart
        </button>
      </div>
    </div>

    <ReviewList v-if="reviews.length" :reviews="reviews"></ReviewList>
    <ReviewForm @review-submitted="addReview"></ReviewForm>
  </div>
</template>

<script>
import blueSocks from "@/assets/images/socks_blue.jpg";
import greenSocks from "@/assets/images/socks_green.jpg";
import ReviewForm from "@/components/review-form.vue";
import ReviewList from "@/components/review-list.vue";

export default {
  name: "ProductDisplay",
  components: {
    ReviewForm,
    ReviewList,
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  data: () => {
    return {
      activeClass: "active-circle",
      product: "Socks",
      brand: "Vue Mastery",
      inventory: 10,
      details: ["50% cotton", "30% wool", "20% ployester"],
      selectedVariant: 0,
      variants: [
        {
          id: 2234,
          color: "green",
          image: greenSocks,
          alt: "Green Socks",
          quantity: 50,
        },
        {
          id: 2235,
          color: "blue",
          image: blueSocks,
          alt: "Blue Socks",
          quantity: 0,
        },
      ],
      reviews: [],
    };
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    src() {
      return this.variants[this.selectedVariant].image;
    },
    alt() {
      return this.variants[this.selectedVariant].alt;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return 2.99;
    },
  },
  methods: {
    // Note: don't use arrow functions on instance properties
    // See: https://v2.vuejs.org/v2/guide/instance.html#Properties-and-Methods
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addReview(review) {
      this.reviews.push(review);
    },
  },
};
</script>

<style>
</style>