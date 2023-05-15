<template>
  <carousel id="carousel-track" :perPage="1" :autoplay="false" :speed="autoplaySpeed">
    <slide class="item" v-for="(release, index) in releases" :key="index">
      <img :id="index" :src="require(`@/assets/images/${release.title}.webp`)" class="image">
      <b-container class="release" fluid align-h="center" align-v="center" @mouseover="autoplay()">
        <b-row>
          <b-col sm="6">
          </b-col>
          <b-col sm="6">
            <h1>{{ release.title }}</h1>
            <h2>{{ release.artist }}</h2>
          </b-col>
        </b-row>
      </b-container>
    </slide>
  </carousel>
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
      currentSlide: 0,
      autoplayTime: 5250,
      autoplayTimeout: null,
      autoplaySpeed: 1250
    }
  },
  methods: {
    carousel() {
      return document.getElementsByClassName("VueCarousel-inner")[0]
    },
    slide(to) {
      to ? this.currentSlide = to : this.currentSlide += 1
      if (this.currentSlide == this.releases.length) this.currentSlide = 0
      this.carousel().style.transform = `translate(-${this.currentSlide * 100}vw, 0px)`
    },
    autoplay(timeout=this.autoplayTime) {
      console.log('clearing')
      clearTimeout(this.autoplayTimeout)
      this.autoplayTimeout = setTimeout(() => {
        this.slide()
        this.autoplay(timeout)
      }, this.autoplayTime)
    }
  },
  watch: {
    currentSlide(n, o) {
      o = document.getElementById(o)
      o.animate(
        { objectPosition: `100% center` },
        { duration: this.autoplaySpeed, fill: 'forwards', easing: 'ease-in-out' }
      )
      n = document.getElementById(n)
      n.animate(
        { objectPosition: `0% center` },
        { duration: 0, fill: 'forwards' }
      )
      n.animate(
        { objectPosition: `${50}% center` },
        { duration: this.autoplaySpeed, fill: 'forwards', easing: 'ease-in-out' }
      )
    }
  },
  mounted() {
    this.autoplay()
  }
}
</script>

<style lang="scss">
.VueCarousel {
  height: 100%;
  pointer-events: none;
  &-wrapper, &-inner {
    height: 100% !important;
  }
  &-pagination {
    display: none;
  }
  .item {
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
    img {
      position: absolute;
      width: 100vw;
      height: 100vh;
      object-fit: cover;
      animation-timing-function: ease-in-out;
      filter: brightness(0.5);
      z-index: -1;
    }
  }
}
</style>
