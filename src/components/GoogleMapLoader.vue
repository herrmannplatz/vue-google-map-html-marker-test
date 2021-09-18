<template>
  <div style="height: 100%">
    <div class="google-map" ref="googleMap"></div>
    <template v-if="Boolean(this.google) && Boolean(this.map)">
      <slot
        :google="google"
        :map="map"
      />
    </template>
  </div>
</template>

<script>
import { Loader } from '@googlemaps/js-api-loader';

export default {
  props: {
    mapConfig: Object,
    apiKey: String,
  },

  data() {
    return {
      google: null,
      map: null
    }
  },

  provide() {
    const loader = {}

    Object.defineProperty(loader, "google", {
        enumerable: true,
        get: () => this.google,
    })

    Object.defineProperty(loader, "map", {
        enumerable: true,
        get: () => this.map,
    })

    return { loader }
  },

  async mounted() {
    const loader = new Loader({ apiKey: this.apiKey, libraries: ["places"] });
    const googleMapApi = await loader.load()
    this.google = googleMapApi

    const mapContainer = this.$refs.googleMap
    this.map = new this.google.maps.Map(mapContainer, this.mapConfig)
  }

}
</script>

<style scoped>
.google-map {
  height: 100%;
}
</style>