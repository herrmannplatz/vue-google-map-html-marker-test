<template>
  <GoogleMapLoader
    :mapConfig="mapConfig"
    :apiKey="null"
  >
    <template slot-scope="{ google, map }">
      <GoogleMapMarker
        v-for="marker in markers"
        :key="marker.id"
        :marker="marker"
        :google="google"
        :map="map"
      >
        <div>
          <button >hello {{ marker.id }}</button>
        </div>
      </GoogleMapMarker>
    </template>
  </GoogleMapLoader>
</template>

<script>
import GoogleMapLoader from "./GoogleMapLoader.vue";
import GoogleMapMarker from "./GoogleMapMarker.vue";

export default {
  components: {
    GoogleMapLoader,
    GoogleMapMarker
  },

  data () {
    return {
      markers: [
        { id: 'Kulturbrauerei', position: { lat: 52.538203, lng: 13.4105247 } },
        { id: 'Wasserturm', position: { lat: 52.5342728, lng: 13.4143335 } }
      ]
    }
  },

  computed: {
    mapConfig () {
      return {
        zoom: 12,
        center: this.mapCenter
      }
    },

    mapCenter () {
      return this.markers[1].position
    }
  },
}
</script>