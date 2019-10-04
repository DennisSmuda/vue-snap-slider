<template>
  <div id="app">
    <header>
      <img alt="Snap Slider Logo" src="./assets/snap-slider-logo.png">
    </header>

    <VueSnapSlider
      :showControls="true"
      :showIndicators="true"
    >
      <div class="slide">
        <h1>1</h1>
      </div>
      <div class="slide">
        <h1>2</h1>
      </div>
      <div class="slide">
        <h1>3</h1>
      </div>
      <div class="slide">
        <h1>4</h1>
      </div>
      <div class="slide">
        <h1>5</h1>
      </div>
      <div class="slide">
        <h1>6</h1>
      </div>

      <!-- TODO: Implement Custom Controls -->
      <!-- <template v-slot:controls>
        <span>Prev</span>
        <span>Next</span>
      </template> -->
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

.slide:nth-child(3),
.slide:nth-child(6) {
  background: #ababab;
}
</style>
