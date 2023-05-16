<template>
  <section class="home-carousel" :style="{ transform: `translate(-${options.currentRelease * 100}vw, 0px)` }" @touchstart="swipestart($event)" @touchend="swipeend($event)">
    <div class="home-carousel-inner">
      <article v-for="(release, index) in releases" :key="index" class="home-carousel-slide">
        <!-- Header -->
        <b-container 
        fluid align-h="center" align-v="center" class="home-carousel-info"
        :style="{ pointerEvents: options.currentRelease == index ? 'all' : 'none'}"> <!-- Prevents the progress bars from draining due to hovering while the carousel moves -->
          <b-row style="height: 18%;" align-v="center">
            <h1 class="highlight uppercase px-5">{{ options.headers[index] }}</h1>
          </b-row>
          <b-row style="height: 64%;" align-v="center">
            <!-- Cover art -->
            <b-col xl="6">
              <b-row class="home-carousel-info--cover">
                <img :src="require(`@/assets/cover/${release.title}.webp`)">
                <h4 class="m-0 p-0"><i>Illustration by⠀<a 
                  :href="release.illustration.url"
                  @mouseover="$emit('pauseplay', index)"
                  @mouseleave="$emit('resumeplay')"
                >⠀{{ release.illustration.artist }}⠀</a></i></h4>
              </b-row>
            </b-col>
            <!-- Info -->
            <b-col xl="6">
              <div class="home-carousel-info--text">
                <h1 class="highlight highlight__white bold">{{ release.title }}</h1>
                <h2>{{ release.artist }}</h2>
                <h3>{{ release.subtitle }}</h3>
                <br>
                <b-row class="home-carousel-info--links m-0">
                  <b-row style="width: auto;" @mouseover="$emit('pauseplay', index)" @mouseleave="$emit('resumeplay')">
                    <a :href="release.url" class="medium-hide" style="width: auto;">
                      <button><h2>⠀Listen⠀</h2></button>
                    </a>
                    <a v-for="(platform, index) in release.platforms" :key="index" :href="platform.url" style="width: auto;">
                      <img :src="require(`@/assets/logos/${platform.name}.webp`)" :alt="platform.name" class="home-carousel-info--icon" v-b-popover.hover.top="platform.name">
                    </a>
                  </b-row>
                </b-row>
              </div>
            </b-col>
          </b-row>
        </b-container>
        <!-- Background image -->
        <img :id="release.title" :src="require(`@/assets/images/${release.title}.webp`)" class="home-carousel-bg">
      </article>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    releases: {
      type: Array,
      required: true
    },
    options: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      touchstartX: null,
      touchstartY: null,
      touchendX: null,
      touchendY: null
    }
  },
  methods: {
    swipestart(event) {
      this.touchstartX = event.changedTouches[0].screenX;
      this.touchstartY = event.changedTouches[0].screenY;
    },
    swipeend(event) {
      this.touchendX = event.changedTouches[0].screenX;
      this.touchendY = event.changedTouches[0].screenY;
      this.handleswipe();
    },
    handleswipe() {
      if (this.touchendX < this.touchstartX) { this.$emit('slide') }        // swiped left
      if (this.touchendX > this.touchstartX) { this.$emit('slide', false) } // swiped right
    }
  },
  watch: {
    'options.currentRelease': {
      handler: function(n, o) {
        o = document.getElementById(this.releases[o].title)
        o.animate(
          { objectPosition: `100% center`, filter: 'brightness(1)'},
          { duration: 1250, fill: 'forwards', easing: 'ease-in-out' }
        )
        n = document.getElementById(this.releases[n].title)
        n.animate(
          { objectPosition: `0% center`, filter: 'brightness(1)'},
          { duration: 0, fill: 'forwards' }
        )
        n.animate(
          { objectPosition: `50% center`, filter: 'brightness(.5)'},
          { duration: 1250, fill: 'forwards', easing: 'ease-in-out' }
        )
      }
    }
  }
}
</script>

<style scoped lang="scss">
.home-carousel {
  width: 100vw;
  transition: 1.25s;
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
    position: absolute;
    height: 100%;
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
          display: none;
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
          max-width: 45vh
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
          font-size: 48px !important;
        }
        h3 {
          font-size: 30px !important;
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