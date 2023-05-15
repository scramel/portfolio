<template>
  <div class="releases-carousel-wrapper">
    <div id="carousel" class="releases-carousel-inner">
      <div v-for="(release, index) in releases" :key="release.title">
        <b-container fluid align-h="center" align-v="center" @mouseover="autoplay()">
          <b-row class="release">
            <b-col xl="6" class="left">
              <img :src="require(`@/assets/cover/${release.title}.webp`)" class="cover">
            </b-col>
            <b-col xl="6" class="right">
              <div class="info">
                <h1>{{ release.title }}</h1>
                <h2>{{ release.artist }}</h2>
                <h2 v-if="release.remix">(Scramel Remix)</h2>
              </div>
            </b-col>
          </b-row>
        </b-container>
        <img :id="index" :src="require(`@/assets/images/${release.title}.webp`)" class="image">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    releases: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      autoplayTime: 5250,
      autoplayTimeout: null,
      currentRelease: 0
    }
  },
  methods: {
    carousel() {
      return document.getElementById("carousel")
    },
    next() {
      this.currentRelease += 1
      if (this.currentRelease == this.releases.length) this.currentRelease = 0
      this.carousel().style.transform = `translate(-${this.currentRelease * 100}vw, 0px)`
    },
    autoplay(timeout=this.autoplayTime) {
      clearTimeout(this.autoplayTimeout)
      this.autoplayTimeout = setTimeout(() => {
        this.next()
        this.autoplay(timeout)
      }, this.autoplayTime)
    }
  },
  watch: {
    currentRelease(n, o) {
      o = document.getElementById(o)
      o.animate(
        { objectPosition: `100% center` },
        { duration: 1250, fill: 'forwards', easing: 'ease-in-out' }
      )
      n = document.getElementById(n)
      n.animate(
        { objectPosition: `0% center` },
        { duration: 0, fill: 'forwards' }
      )
      n.animate(
        { objectPosition: `50% center` },
        { duration: 1250, fill: 'forwards', easing: 'ease-in-out' }
      )
    }
  },
  mounted() {
    this.autoplay()
  }
}
</script>

<style scoped lang="scss">
.releases-carousel {
  &-wrapper {
    width: 100vw;
    height: 100%;
    overflow: hidden;
    position: relative;
  }
  &-inner {
    width: 100vw;
    height: 100%;
    display: flex;
    transition: 1.25s;
    position: absolute;
    .image {
      height: 100vh;
      width: 100vw;
      object-fit: cover;
      filter: blur(.1rem) brightness(.5);
      animation-timing-function: ease-in-out;
    }
    .cover {
      max-height: 70vh;
      max-width: 80vw;
    }
    .release {
      display: flex;
      justify-content: center;
      align-items: center;
      position: absolute;
      height: 100%;
      width: 100%;
      z-index: 1;
      @media only screen and (max-width: 1200px) { // Small only
        margin-top: 10vh;
      }
      .left, .right {
        justify-content: center;
        align-items: center;
        @media only screen and (min-width: 1200px) { // XL only
          img {
            margin-left: 20vw;
          }
          .info {
            padding: 1rem;
            text-align: left;
          }
        }
        @media only screen and (max-width: 1200px) { // Small only
          img {
            height: 60vh;
            object-fit: contain;
          }
          height: 50%;
          width: 100%;
        }
      }
      .right {
        .info {
          background-color: rgba(0, 0, 0, .5);
          h1 {
            font-size: 5rem;
          }
          h1, h2 {
            filter: drop-shadow(0 0 0.1rem #000);
            text-shadow: #000 1px 0 .5vw;
            margin: 0;
          }
        }
        @media only screen and (max-width: 1200px) { // Small only
          margin-top: 10vw;
          .info {
            h1 {
              font-size: 3rem;
            }
          }
        }
      }
    }
  }
}
</style>
