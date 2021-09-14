<template>
  <div id="app">
    <vue-google-map />
  </div>
</template>

<script>
import VueGoogleMap from './components/VueGoogleMap.vue'

export default {
  name: 'App',
  components: {
    VueGoogleMap
  }
}
</script>

<style>
#app {
  height: 100vh;
}
</style>
