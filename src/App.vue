<template>
  <div id="app">
    <NavBar/>
    <router-view/>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue'

export default {
  components: {
    NavBar
  }
}
</script>

<style lang="scss">
@font-face {
  font-family: Sanseriffic;
  src: url('@/assets/fonts/Sanseriffic.otf')
}
@font-face {
  font-family: BubblerOne;
  src: url('@/assets/fonts/BubblerOne-Regular.ttf')
}


#app {
  font-family: BubblerOne;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  height: 100%;
}
*, body {
  margin: 0;
  padding: 0;
}
body {
  height: 100vh;
  background-color: black !important;
}

h1, h2, h3, h4, h5, h6 {
  margin: auto !important;
  width: auto !important;
}
h1 {
  font-size: 60px !important;
}
h2 {
  font-size: 48px !important;
}
h3 {
  font-size: 36px !important;
}
h4 {
  font-size: 30px !important;
}
p {
  font-size: 24px !important;
}

// A few global classes to make life easier
.uppercase {
  text-transform: uppercase;
}
.bold {
  font-weight: bold;
}
.highlight {
  padding-top: 6px;
  background: black;
  &__white {
    padding-top: 0;
    background: white;
    color: black;
    display: inline-block;
  }
}
.small-hide {
  @media only screen and (max-width: 699px) { // Small only
    display: none !important;
  }
}
.medium-hide {
  @media only screen and (max-width: 1199px) { // Small only
    display: none !important;
  }
}


// Bootstrap progress bar
.progress {
  border: 1px solid white;
  border-radius: 0 !important;
  background-color: transparent !important;
}
.progress-bar {
  background-color: white !important;
}

// Bootstrap tooltip
.popover.b-popover {
  margin-bottom: 6px;
  .popover-body {
    font-family: BubblerOne;
    font-size: 24px;
    padding: 5px 10px;
  }
}

// Custom scrollbar
::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
  background-color: black;
  border-right: solid white 1px;
}
::-webkit-scrollbar {
  background: #F5F5F5;
  width: 6px;
}
::-webkit-scrollbar-thumb {
  background-color: white;
}
</style>
