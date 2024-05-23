<template>
  <div id="app">
    <NavBar/>
    <router-view/>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar.vue'

// .sample() custom function
Array.prototype.sample = function(){
  return this[Math.floor(Math.random()*this.length)];
}

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
h1 { font-size: 60px !important; }
h2 { font-size: 48px !important; }
h3 { font-size: 36px !important; }
h4 { font-size: 30px !important; }
p { font-size: 24px !important; }

@media only screen and (max-width: 699px) { // Small only
  h1 { font-size: 40px !important; }
  h2 { font-size: 32px !important; }
  h3 { font-size: 26px !important; }
  h4 { font-size: 24px !important; }
  p { font-size: 24px !important; }
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

// hide / show
.sm-show {
  @media only screen and (max-width: 699px) {
    display: none !important;
  }
}
.sm-hide {
  display: none !important;
  @media only screen and (max-width: 699px) {
    display: flex;
  }
}
.md-show {
  @media only screen and (max-width: 1199px) {
    display: none !important;
  }
}
.md-hide {
  display: none !important;
  pointer-events: none;
  @media only screen and (max-width: 1199px) {
    display: flex !important;
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

// Transitions!
.typing-enter-active {
  animation:
  typing 1s steps(16, end),
  typecursor .35s step-end infinite;
}
.typing-leave-active {
  animation:
  typing .5s steps(10, end) reverse,
  typecursor .3s step-end infinite;
}
@keyframes typing {
  from { width: 0 }
  to { width: 100%; }
}
@keyframes typecursor {
  from, to { border-color: #fff; }
  50% { border-color: transparent; }
}

@keyframes slidein-next {
  0% { transform: translateX(5vh); opacity: 0; }
  100% { transform: translateX(0); opacity: 1; }
}
@keyframes slideout-next {
  0% { transform: translateX(0); opacity: 1; }
  100% { transform: translateX(-5vh); opacity: 0; }
}
@keyframes slidein-prev {
  0% { transform: translateX(-5vh); opacity: 0; }
  100% { transform: translateX(0); opacity: 1; }
}
@keyframes slideout-prev {
  0% { transform: translateX(0); opacity: 1; }
  100% { transform: translateX(5vh); opacity: 0; }
}

.slide-fade {
  // maybe could use just one animation and adjust the parameters with variables
  &-enter-true { animation: slidein-next .4s forwards ease-out; }
  &-leave-true { animation: slideout-next .3s forwards ease-in; }
  &-enter-false { animation: slidein-prev .4s forwards ease-out; }
  &-leave-false { animation: slideout-prev .3s forwards ease-in; }
}
</style>
