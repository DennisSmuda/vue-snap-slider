<template>
  <div id="app">
    <header>
      <img alt="Snap Slider Logo" src="./assets/snap-slider-logo.png">
    </header>

    <VueSnapSlider>
      <div class="slide">
        Butz
      </div>
      <div class="slide">
        Butz 2
      </div>
      <div class="slide">
        Butz 2
      </div>
    </VueSnapSlider>
  </div>
</template>

<script>
import VueSnapSlider from './components/VueSnapSlider.vue'

export default {
  name: 'app',
  components: {
    VueSnapSlider
  }
}
</script>

<style>
#app {
  font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

header {
  display: flex;
  height: 7rem;
}

header img {
  height: 100%;
  width: auto;
}

.slide:nth-child(1),
.slide:nth-child(4) {
  background: #e2e2e2;
}

.slide:nth-child(2),
.slide:nth-child(5) {
  background: #c3c3c3;
}

.slide:nth-child(3) {
  background: #ababab;
}
</style>
