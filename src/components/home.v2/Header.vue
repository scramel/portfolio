<template>
	<header class="home-header" v-if="tracklist.length">
		<Background :imgs="tracklist.map(el => el.title)" :current="current"/>
		<!-- Tracklist -->
		<b-row class="home-tracklist md-show">
			<ProgressBar v-for="(track, index) in tracklist"
				:key="index"
				:index="index"
				:current="current"
				:tag="track.tag"
				:title="track.title"
				class="mx-4"
				@onClick="current = index"
				@onFull="advanceCurrentTrack()"
			/>
		</b-row>
		<!-- Solo track -->
		<b-row class="home-tracklist md-hide">
			<ProgressBar :index="-1" :current="current" :tag="tracklist[current].tag" :title="tracklist[current].title" :mobile="true" class="mx-4"/>
		</b-row>
	</header>
</template>

<script>
import Background from '@/components/home.v2/components/Background.vue'
import ProgressBar from '@/components/home.v2/components/ProgressBar.vue'
import releases from './releases.js'

export default {
  components: {
    ProgressBar,
		Background
  },
  data() {
    return {
			tracklist: [],
			current: 0,
      carouselTimeout: null,
		}
	},
	methods: {
    advanceCurrentTrack() {
			if (this.current < 2) return this.current++
			this.current = 0
		}
	},
  mounted() {
    this.tracklist = [
      { ...releases.latest.sample(), tag: "Latest" }, // random latest
      { ...releases.popular.sample(), tag: "Popular" }, // random popular
      { ...releases.featured.sample(), tag: "Featured" } // random featured
    ]
  }
}
</script>

<style lang="scss">
.home {
  &-header {
    overflow: hidden;
		max-height: 100vh;
		max-width: 100vw;
		background-color: rgb(0, 0, 0);
  }
  &-tracklist {
    position: absolute;
    z-index: 1;
    display: flex;
    min-width: 100%;
		// height: 10vh;
		height: auto;
		// margin-bottom: 5vh;
		// bottom: 0;
		bottom: 5vh;
		--bs-gutter-x: 0 !important;
		&-group {
			@media only screen and (max-width: 1199px) { // Small only
				display: none !important;
			}
		}
		&-solo {
			display: none !important;
			@media only screen and (max-width: 1199px) { // Small only
				display: flex !important;
			}
		}
  }
}
</style>