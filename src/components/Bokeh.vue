<template>
  <div id="bokeh">
    <div v-for="(bokeh, index) in density" :key="index" class="bokeh"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      density: 15
    }
  }
}
</script>

<style lang="scss" scoped>
#bokeh {
  height: 100vh;
  width: 100vw;
  // background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
  overflow: hidden;
  position: fixed;
  // filter: drop-shadow(0 0 10px rgb(75, 75, 0));
  z-index: 1;
  // transform: rotate(180deg);
  mix-blend-mode: color-dodge;
}

@function random_range($min, $max) {
  $rand: random();
  $random_range: $min + floor($rand * (($max - $min) + 1));
  @return $random_range;
}

.bokeh {
  $total: 15;
  position: absolute;
  width: .4vh;
  height: .4vh;
  background: rgb(20, 15, 10);
  border-radius: 50%;

  @for $i from 1 through $total {
    $random-x: random(1000000) * 0.0001vw;
    $random-offset: random_range(-100000, 100000) * 0.0001vw;
    $random-x-end: $random-x + $random-offset;
    $random-x-end-yoyo: $random-x + ($random-offset / 2);
    $random-yoyo-time: random_range(30000, 80000) / 100000;
    $random-yoyo-y: $random-yoyo-time * 100vh;
    $random-scale: random(10000) * 0.01;
    $fall-duration: random_range(10, 30) * 2.5s;
    $fall-delay: random(30) * -1s;

    &:nth-child(#{$i}) {
      opacity: 1;
      transform: translate($random-x, -10px) scale($random-scale);
      animation: fall-#{$i} $fall-duration $fall-delay linear infinite;
    }

    @keyframes fall-#{$i} {
      #{percentage($random-yoyo-time)} {
        transform: translate($random-x-end, $random-yoyo-y) scale($random-scale);
      }

      to {
        transform: translate($random-x-end-yoyo, 100vh) scale($random-scale);
      }
    }
  }
}
</style>
