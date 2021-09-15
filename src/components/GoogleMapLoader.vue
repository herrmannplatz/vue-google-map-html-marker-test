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
import GoogleMapsApiLoader from 'google-maps-api-loader'

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
    const google = {}

    Object.defineProperty(google, "api", {
        enumerable: true,
        get: () => this.google,
    })

    Object.defineProperty(google, "map", {
        enumerable: true,
        get: () => this.map,
    })

    return { google }
  },

  async mounted() {
    const googleMapApi = await GoogleMapsApiLoader({ apiKey: this.apiKey })
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