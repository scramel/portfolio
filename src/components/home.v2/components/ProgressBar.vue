<template>
  <b-col class="home-progress-bar" @click="$emit('onClick')">
    <Transition name="typing">
      <div class="home-progress-bar-textbox" v-if="show">
        <p><b class="uppercase">{{ tag }}:</b> {{ title }}</p>
      </div>
    </Transition>
    <b-progress :id="index" height="7px" :value="0"></b-progress>
  </b-col>
</template>

<script>
export default {
  props: {
    index: { // track number
      type: Number,
      required: true
    },
    current: { // currently displaying track
      type: Number,
      required: true
    },
    tag: { // latest/popular/featured
      type: String,
      required: true
    },
    title: { // track title
      type: String,
      required: true
    },
    mobile: { // for mobile displays
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      timer: undefined,
      fillTime: 5250,
      drainTime: 500,
      show: true
    }
  },
  methods: {
    manageBar(id) {
      let bar = document.getElementById(this.index) // progress bar element
      if (!bar || !bar.children[0]) return setTimeout(() => this.manageBar(id), 500) // if the element hasn't loaded yet, retry .5s later
      bar = bar.children[0] // bar fill element
      if (this.mobile) {
        this.show = true
        this.fill(bar, "100", this.fillTime, 'linear')
        this.timer = setTimeout(() => {
          this.show = false
          this.fill(bar, "0", this.drainTime)
      }, this.fillTime)
        return
      }
      if (id > this.index) return this.fill(bar, "100", this.drainTime) // if the current track is above this one, full the bar
      this.fill(bar, "0", this.drainTime) // else, drain the bar
      if (id < this.index) return // if the current track is below this one, leave it at that
      setTimeout(() => { // normally the progress bar stutters without this timeout because it tries to drain and then fill itself at the same time
        this.fill(bar, "0", 0) // this avoids easing: ease-in for the next line and i have no idea why
        this.fill(bar, "100", this.fillTime, 'linear', true) // if the current track is this one, fill the bar at normal speed
      }, this.drainTime)
    },
    fill(bar, width, duration, easing='ease-in-out', timer=false) {
      bar.animate(
        { width: `${width}%` }, { 
          duration,
          easing,
          fill: 'forwards'
        }
      )
      if (!timer) return clearTimeout(this.timer)
      this.timer = setTimeout(() => { // this timer is what tells the app to jump onto the next track
        if (this.index == this.current) this.$emit('onFull')
      }, this.fillTime)
    }
  },
  watch: {
    current: {
      deep: true,
      immediate: true,
      handler: function(n) {
        this.manageBar(n)
      }
    }
  }
}
</script>

<style lang="scss">
.home-progress-bar {
	padding-top: 10px;
	padding-bottom: 20px;
  padding-left: 20px !important;
  padding-right: 20px !important;
  transition: .1s;
  &-textbox {
    white-space: nowrap; /* Keeps the content on a single line */
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    max-width: max-content;
    @media only screen and (max-width: 1199px) { // Small only
      border-right: 10px solid #ffffff00;
    }
    p {
      text-align: left;
      margin: 0;
    }
  }
  .col {
    text-align: left;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .progress {
    width: 100%;
  }
  &:hover {
		cursor: pointer;
		background-color: rgba(255, 255, 255, 0.15);
	}
  &:active {
    transition: .0s;
		background-color: rgba(255, 255, 255, 0.25);
  }
}
</style>