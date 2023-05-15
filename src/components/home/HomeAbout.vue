<template>
  <section id="about" class="home-about">
    <div class="container pt-5">
      <b-row>
        <h1 class="highlight highlight__white uppercase px-5">About</h1>
      </b-row>
      <b-row class="py-5 home-about-lorem" xl="5">
        <b-col>
          <img :src="require(`@/assets/logos/scramel.webp`)" class="logo">
          <b-row class="my-4" style="width: 100%;">
            <button :class="tab ? 'active' : ''" @click="tab = true" style="margin-right: 1rem;">
              <h3>Music</h3>
            </button>
            <button :class="tab ? '' : 'active'" @click="tab = false">
              <h3>Web dev</h3>
            </button>
          </b-row>
        </b-col>
        <b-col xl="7">
          <div v-if="tab">
            <p>
              Hobbyist <b>FL Studio 20</b> user, passionate about remixing my favourite tunes and yearning to work in
              the professional industry - especially soundtracks for games. Almost all my knowledge has been
              self-taught, but I'm looking to study music production and get a degree sooner or later.
            </p>
            <p>
              Pioneering <a href="https://www.youtube.com/watch?v=cKAFFarrosM"><i>neoclassic trance</i> </a> as
              a genre, inspired by japanese musicians such as zts and Taishi. I love making trance, rock, and
              metal, but I'm also comfortable with other genres such as lo-fi, hardcore, ambient, electro swing,
              fusion jazz, darksynth. My style mostly relies on using acoustic and percussive instrument sounds
              while combining them with electronic beats.
            </p>
          </div>
          <div v-else>
            <p>
              Web application development specialist with three of work experience and knowledge of HTML5,
              CSS/SCSS, JavaScript, Vue.js 2 and 3, Ruby/Ruby on Rails, React.js, Git, SQL, Bootstrap, Postman,
              Firebase , consumption of APIs, modeling and management of databases with PostgreSQL and MySQL.
              Good intuition for interface design and user experience (UI/UX).
            </p>
            <p>
              Three years of work experience with <b>Vue.js</b> and its tools such as VueRouter, Vuex, Nuxt,
              Element UI, and BootstrapVue, and also with with <b>Ruby on Rails</b> developing both applications
              that follow the MVC pattern and mostly REST API applications, with knowledge in unit tests with
              RSPec and deployments with Capistrano.
            </p>
          </div>
        </b-col>
      </b-row>
    </div>
    <img :src="require('@/assets/textures/hana.webp')" alt="Hana" class="flowers flowers-left">
    <img :src="require('@/assets/textures/hana.webp')" alt="Hana" class="flowers flowers-right">
  </section>
</template>

<script>
export default {
  data() {
    return {
      tab: true
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  &-about {
    overflow: hidden;
    position: relative;
    /* The image used */
    background-image: url(@/assets/textures/stars.webp);
    /* Create the parallax scrolling effect */
    background-attachment: fixed;
    background-position: center;
    background-repeat: repeat;
    // Infinite background scrolling
    animation: scroll 100s linear infinite;
    // full height
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    justify-content: center;
    @keyframes scroll {
      100% {
        background-position: -200% 100%;
      }
    }
    &-lorem {
      align-items: center;
      div { justify-content: center; }
      a { color: white; }
      button {
        text-align: center;
        width: auto;
        background: transparent;
        color: white;
        border: solid 1px white;
        transition: .2s;
        &.active, &:hover, &:active {
          background: white;
          color: black;
        }
      }
    }
    .logo {
      max-height: 40vh;
      max-width: 50vh;
      width: auto;
      object-fit: contain;
    }
    p {
      text-indent: 50px;
      text-align: justify;
      margin-right: 6vw;
      @media only screen and (max-width: 1200px) { // Small only
        margin-left: 6vw;
      }
    }
    .flowers {
      top: 0;
      position: absolute;
      width: 10vw;
      height: 100%;
      object-fit: cover;
      display: none;
      &-left { left: 0; }
      &-right {
        right: 0;
        transform: rotate(180deg);
      }
      @media only screen and (max-width: 767px) { // Small only
        display: none;
      }
    }
  }
}
</style>