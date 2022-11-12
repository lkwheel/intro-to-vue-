<template>
  <img
    :src="computedSrc"
    :alt="alt"
    class="BaseImage"
    v-bind="$attrs"
  />
</template>
      
      <script>
export default {
  name: "BaseImage",

  inheritAttrs: false,

  props: {
    src: {
      type: String,
      required: true,
    },

    /**
     * The alt tag is required for accessibility and SEO purposes.
     *
     * If it is a decorative image, which is purely there for design reasons,
     * consider moving it to CSS or using an empty alt tag.
     */
    alt: {
      type: String,
      required: true,
    },
  },

  computed: {
    // If the URL starts with @/assets/, it will be interpreted as a module request.
    isModuleRequest() {
      return this.src.startsWith("@/assets/images/");
    },

    computedSrc() {
      // If it is a module request,
      // the exact module is not known on compile time,
      // so an expression is used in the request to create a context.
      return this.isModuleRequest
        ? require(`../assets/${this.src.replace("@/assets/images/", "")}`)
        : this.src;
    },
  },
};
</script>