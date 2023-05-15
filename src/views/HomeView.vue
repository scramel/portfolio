<template>
  <main class="home scrollbar">
    <HomeHeader id="header"/>
    <!-- <HomeAbout id="about"/> -->
  </main>
</template>

<script>
import HomeHeader from '@/components/home/HomeHeader.vue'
// import HomeAbout from '@/components/home/HomeAbout.vue'

export default {
  name: 'HomeView',
  components: {
    HomeHeader
   // HomeAbout
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.home, header {
  height: 100%;
}
</style>
