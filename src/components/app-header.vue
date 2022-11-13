<template>
  <div class="nav-bar">
    <span class="nav-bar-container">
      <button class="nav-bar-button" v-show="loggedIn">Logout</button>
    </span>
  </div>
</template>
<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      loggedIn: false,
    };
  },
};
</script>
<style lang="">
</style>