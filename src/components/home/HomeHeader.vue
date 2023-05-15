<template>
  <header class="home-header">
      <section class="home-buttons">
        <b-row class="home-buttons" style="margin-top: 82vh; height: 18vh;">
          <HomeProgressBar v-for="(release, index) in selection" :key="index" :header="options.headers[index]" :title="release.title" :index="index" class="mx-5"/>
        </b-row>
      </section>
      <HomeCarousel :releases="selection" :options="options" @pauseplay="pauseTimer($event)" @resumeplay="autoplay(options.currentRelease)"/>
  </header>
</template>

<script>
import HomeCarousel from '@/components/home/HomeCarousel.vue'
import HomeProgressBar from '@/components/home/HomeProgressBar.vue'

export default {
  components: {
    HomeCarousel,
    HomeProgressBar
  },
  data() {
    return {
      selection: [],
      autoplayDelay: 5250,
      autoplayTimeout: null,
      options: {
        headers: ['Latest', 'Popular', 'Featured'],
        currentRelease: 0
      },
      releases: {
        latest: [{
          title: "the executioner",
          artist: "zts",
          subtitle: "(Metal Remix)",
          url: "https://www.youtube.com/watch?v=2y4ETS9WIfw",
          platforms: [{
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=2y4ETS9WIfw"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/the-executioner"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/track/the-executioner"
          }],
          illustration: {
            artist: "Natsumi Kei",
            url: "https://twitter.com/sirius1810405"
          }
        }, {
          title: "シューニャの空",
          artist: "xaki",
          subtitle: "(Trance Remix)",
          url: "https://www.youtube.com/watch?v=5Rk-lYnlmVA",
          platforms: [{
            name: "Website",
            url: "https://fragmentsofgratitude.tumblr.com"
          }, {
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=5Rk-lYnlmVA"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/sunya-no-sora"
          }, {
            name: "Bandcamp",
            url: "https://kodamasounds.bandcamp.com/track/nya-no-sora-emptinesss-sky"
          }],
          illustration: {
            artist: "KUYA",
            url: "https://twitter.com/hey36253625"
          }
        }],
        popular: [{
          title: "goldenslaughterer",
          artist: "zts",
          subtitle: "(Electro Swing Remix)",
          url: "https://www.youtube.com/watch?v=uK0ZV_PyFeU",
          platforms: [{
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=uK0ZV_PyFeU"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/goldenslaughterer"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/track/goldenslaughterer"
          }, {
            name: "Spotify",
            url: "https://open.spotify.com/album/60uASpAmlDVxNsuhILNTFl"
          }],
          illustration: {
            artist: "@Azuminkun",
            url: "https://twitter.com/azuminkun"
          }
        }, {
          title: "BIG SHOT",
          artist: "Toby Fox",
          subtitle: "(Dance Remix)",
          url: "https://www.youtube.com/watch?v=GLUYD4NcC4k",
          platforms: [{
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=GLUYD4NcC4k"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/big-shot"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/track/big-shot"
          }],
          illustration: {
            artist: "@marshukitty",
            url: "https://twitter.com/marshukitty"
          }
        }, {
          title: "牢獄STRIP",
          artist: "-45",
          subtitle: "(Fusion Jazz Remix)",
          url: "https://www.youtube.com/watch?v=tfbSUKRO5cQ",
          platforms: [{
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=tfbSUKRO5cQ"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/our-prison"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/track/our-prison"
          }, {
            name: "Spotify",
            url: "https://open.spotify.com/album/60uASpAmlDVxNsuhILNTFl"
          }],
          illustration: {
            artist: "@gativ0",
            url: "https://twitter.com/gativ0"
          }
        }],
        featured: [{
          title: "hope",
          artist: "dai",
          subtitle: "(Neoclassic Trance Remix)",
          url: "https://www.youtube.com/watch?v=cKAFFarrosM",
          platforms: [{
            name: "Website",
            url: "https://fragmentsofgratitude.tumblr.com/"
          }, {
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=cKAFFarrosM"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/hope"
          }, {
            name: "Bandcamp",
            url: "https://kodamasounds.bandcamp.com/track/hope"
          }],
          illustration: {
            artist: "KUYA",
            url: "https://twitter.com/hey36253625"
          }
        }, {
          title: "Luna Nova",
          artist: "Scramel & SCAR",
          subtitle: "(Ambient Album)",
          url: "https://www.youtube.com/watch?v=VEHaAqhIuMA",
          platforms: [{
            name: "Website",
            url: "https://scramel.github.io/luna-nova"
          }, {
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=VEHaAqhIuMA"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/sets/luna-nova"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/album/luna-nova"
          }, {
            name: "Spotify",
            url: "https://open.spotify.com/album/0hxqwP1rSCFFexiMBvssDr"
          }],
          illustration: {
            artist: "me!",
            url: "https://twitter.com/scramelworks"
          }
        }, {
          title: "Girl Next Door",
          artist: "Toby Fox",
          subtitle: "(Lo-fi Remix)",
          url: "https://www.youtube.com/watch?v=ausxySLlim8",
          platforms: [{
            name: "YouTube",
            url: "https://www.youtube.com/watch?v=ausxySLlim8"
          }, {
            name: "SoundCloud",
            url: "https://soundcloud.com/scramel/girl-next-door"
          }, {
            name: "Bandcamp",
            url: "https://scramel.bandcamp.com/track/girl-next-door"
          }],
          illustration: {
            artist: "gativ0",
            url: "https://twitter.com/gativ0"
          }
        }]
      }
    }
  },
  methods: {
    next() { // shows the next slide in the carousel
      this.options.currentRelease += 1
      if (this.options.currentRelease == this.selection.length) this.options.currentRelease = 0
    },
    loop() { // drains all the progress bars
      this.selection.forEach((el, index) => {
        const progressbar = document.getElementById(index)
        progressbar.children[0].animate(
          { width: `0%` },
          { duration: 500, fill: 'forwards', easing: 'ease-in-out' }
        )
      })
    },
    startTimer(timeout=this.autoplayDelay) { // starts a timer before getting to next slide
      clearTimeout(this.autoplayTimeout)
      this.autoplayTimeout = setTimeout(() => {
        this.next()
      }, timeout)
    },
    pauseTimer(index) { // stops the timer and drains the progress bar for the current slide
      clearTimeout(this.autoplayTimeout)
      const progressbar = document.getElementById(index)
      progressbar.children[0].animate(
        { width: `0%` },
        { duration: 500, fill: 'forwards' }
      )
    },
    autoplay(index) { // starts a timer and starts filling the current progress bar
      const progressbar = document.getElementById(index)
      if (!progressbar) return setTimeout(() => this.autoplay(index), 1000);
      this.startTimer()
      progressbar.children[0].animate(
        { width: `100%` },
        { duration: this.autoplayDelay, fill: 'forwards' }
      )
    }
  },
  watch: {
    'options.currentRelease': { // sets up a timer and progress bar after the carousel reaches a new slide
      immediate: true,
      handler: function(n, o) {
        if (n == 0 && o == 2) this.loop() // if the end of the carousel was reached, loops to the beginning
        this.autoplay(n)
      }
    }
  },
  mounted() {
    this.selection = [
      this.releases.latest[Math.floor(Math.random() * this.releases.latest.length)], // random latest
      this.releases.popular[Math.floor(Math.random() * this.releases.popular.length)], // random popular
      this.releases.featured[Math.floor(Math.random() * this.releases.featured.length)] // random featured
    ]
  }
}
</script>

<style lang="scss">
.home {
  &-header {
    overflow: hidden;
  }
  &-buttons {
    position: absolute;
    z-index: 1;
    display: flex;
    width: 100%;
    @media only screen and (max-width: 1199px) { // Small only
      display: none;
    }
    .row {
      p {
        width: 100%;
        margin: 0;
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
    }
  }
}
</style>