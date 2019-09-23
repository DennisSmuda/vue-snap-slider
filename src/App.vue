<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <VueSnapSlider>
      <div class="slide">
        Butz
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
  margin-top: 60px;
}
</style>
