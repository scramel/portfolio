<template>
  <nav class="navbar">
    <b-row class="mx-5" style="width: 100%;">
      <b-row class="p-0 medium-hide">
        <img class="navbar-logo" :src="require('@/assets/logos/scramel.webp')" alt="Logo" @click="scrollTo()">
        <p>music production<br>& web development</p>
      </b-row>
    </b-row>
  </nav>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav> -->
</template>

<script>
export default {
  methods: {
    scrollTo(id="about") {
      document.getElementById(id).scrollIntoView()
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  position: fixed;
  z-index: 1;
  width: 100%;
  padding: 0;
  display: flex;
  height: 18vh;
  pointer-events: none;
  p {
    margin: 0 !important;
    width: auto;
    line-height: 1.2;
    align-self: center;
    text-align: left;
  }
  .row {
    padding: 0;
    margin: 0;
  }
  &-logo {
    background: black;
    height: 80px;
    padding: 8px;
    cursor: pointer;
    pointer-events: all;
    width: auto;
  }
}
</style>