<template>
  <Transition name="slide-fade">
    <b-container v-show="show" fluid align-h="center" align-v="center" class="home-carousel-info" :class="slideFadeClass"
    :style="{ pointerEvents: disablePointerEvents}"> <!-- Prevents the progress bars from draining due to hovering while the carousel moves -->
      <b-row style="height: 18%;" align-v="center">
        <h1 class="highlight uppercase px-5">{{ tracklist[trueCurrent].tag }}</h1>
      </b-row>
      <b-row style="height: 64%; margin-top: 5vh;" align-v="center">
        <!-- Cover art -->
        <b-col xl="6">
          <b-row class="home-carousel-info--cover">
            <img v-show="index === trueCurrent" v-for="(track, index) in tracklist" :key="index" :src="require(`@/assets/cover/${track.title}.webp`)">
            <h4 class="m-0 p-0"><i>Illustration by⠀<a 
              :href="tracklist[trueCurrent].illustration.url"
              @mouseover="$emit('pauseplay')"
              @mouseleave="$emit('resumeplay')"
            >⠀{{ tracklist[trueCurrent].illustration.artist }}⠀</a></i></h4>
          </b-row>
        </b-col>
        <!-- Info -->
        <b-col xl="6">
          <div class="home-carousel-info--text">
            <div>
              <h1 class="highlight highlight__white bold">{{ tracklist[trueCurrent].title }}</h1>
              <h2 class="md-show">{{ tracklist[trueCurrent].artist }}</h2>
              <h3 class="md-show">{{ tracklist[trueCurrent].subtitle }}</h3>
            </div>
            <br>
            <b-row class="home-carousel-info--links m-0">
              <b-row style="width: auto;" @mouseover="$emit('pauseplay')" @mouseleave="$emit('resumeplay')">
                <a class="md-show" :href="tracklist[trueCurrent].url" style="width: auto;">
                  <!-- <button><h2>⠀Preview⠀</h2></button> -->
                  <button><h2>⠀Listen⠀</h2></button>
                </a>
                <a v-for="(platform, index) in tracklist[trueCurrent].platforms" :key="index" :href="platform.url" style="width: auto;">
                  <img :src="require(`@/assets/logos/${platform.name}.webp`)" :alt="platform.name" class="home-carousel-info--icon" v-b-popover.hover.top="platform.name">
                </a>
              </b-row>
            </b-row>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </Transition>
</template>

<script>
export default {
  props: {
    tracklist: {
      type: Array,
      required: true
    },
    current: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      disablePointerEvents: false,
      show: true,
      trueCurrent: 0,
      direction: true, // if 'true' moves right. if 'false' moves left.
    }
  },
  computed: {
    slideFadeClass() { // dynamic transition class name
      return this.show ? `slide-fade-enter-${this.direction}` : `slide-fade-leave-${this.direction}`
    }
  },
  watch: {
    current(n, o) {
      if (n === o) return
      this.show = false
      this.direction = n > o
      setTimeout(() => {
        this.trueCurrent = this.current
        this.show = true
      }, 500);
    }
  }
}
</script>

<style scoped lang="scss">
.home-carousel {
  &-slide {
    position: relative;
    width: 100vw;
    height: 100vh;
  }
  &-inner {
    display: flex;
    position: absolute;
  }
  &-bg {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    filter: brightness(.5);
    animation-timing-function: ease-in-out;
  }
  &-info {
    z-index: 1;
    position: fixed;
    width: 100vw;
    height: 85vh;
    transition: 1.25s;
    display: flex;
    flex-direction: column;
    &--cover {
      flex-direction: row-reverse;
      @media only screen and (max-width: 1199px) { // Small only
        justify-content: center;
      }
      h4 {
        writing-mode: vertical-rl;
        transform: rotate(180deg);
        @media only screen and (max-width: 699px) { // Small only
          writing-mode: horizontal-tb;
          transform: rotate(0deg);
        }
      }
      img {
        max-height: 64vh;
        width: auto;
        object-fit: contain;
        @media only screen and (min-width: 700px) { // Med only
          max-width: min(60vw, 50vh);
        }
        @media only screen and (min-width: 1200px) { // Big only
          max-width: 45vw;
        }
        @media only screen and (max-width: 699px) { // Small only
          max-width: 75vw;
          max-height: 45vh;
          margin-bottom: 1vh;
          margin: 0 25vw;
        }
      }
      a {
        color: white;
        transition: .2s;
        &:hover {
          color: black;
          background: white;
          text-decoration-color: white;
        }
      }
    }
    &--text {
      text-align: left;
      h1 {
        padding: 0 40px;
      }
      a {
        align-self: center;
        justify-content: center;
        margin-right: 14px;
        padding: 0;
      }
      @media only screen and (max-width: 1199px) { // Small only
        h1 {
          padding: 0 10px;
        }
        margin-top: 1rem;
        text-align: center;
      }
    }
    &--links {
      @media only screen and (max-width: 1199px) { // Small only
        justify-content: center;
      }
    }
    &--icon {
      display: flex;
      height: 40px;
    }
    button {
      border: 2px solid white;
      background: transparent;
      color: white;
      width: auto;
      padding-top: 4px;
      transition: .2s;
      h3 { font-weight: bold; }
      &:hover {
        padding-left: 30px;
        padding-right: 30px;
      }
      @media only screen and (max-width: 1199px) { // Small only
        margin: auto;
      }
    }
  }
}
</style>