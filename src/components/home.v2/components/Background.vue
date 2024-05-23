<template>
  <div class="home-background">
    <div class="home-gradient"></div>
    <div class="home-viewport" :style="{right: pos}">
      <img v-for="(img, index) in imgs" :key="img" :src="require(`@/assets/images/${img}.webp`)" :style="{
        objectPosition: `${calcObjPos(index)}%`
      }">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      objPos: 58,
      offset: 10
    }
  },
  methods: {
    calcObjPos(index) {
      if (index === this.current) return this.objPos
      return index < this.current ? this.objPos + this.offset : this.objPos - this.offset
    }
  },
  computed: {
    pos() {
      return `${this.current}00vw`
    }
  },
  props: {
    imgs: {
      type: Array,
      required: true
    },
    current: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="scss">
.home {
  &-background {
    min-height: 100vh;
    min-width: 300vw;
    overflow: hidden;
    position: fixed;
  }
  &-viewport {
    position: relative;
    transition: 1s;
    overflow: hidden;
    display: flex;
    img {
      transition: 1s;
      height: 100vh;
      width: 100vw;
      object-fit: cover;
      filter: brightness(.6);
    }
  }
  &-gradient {
    background: linear-gradient(0deg, rgba(0, 0, 0, .75) 0%, rgba(0, 0, 0, 0) 25%, rgba(0, 0, 0, 0) 100%);
    height: 100vh;
    width: 100vw;
    position: absolute;
    z-index: 1;
    mix-blend-mode: darken;
  }
}
</style>
