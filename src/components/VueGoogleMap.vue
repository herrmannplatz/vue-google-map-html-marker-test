<template>
  <GoogleMapLoader
    :mapConfig="mapConfig"
    :apiKey="null"
  >
    <GoogleMapMarker
      v-for="marker in markers"
      :key="marker.id"
      :marker="marker"
    >
      <div class="marker"></div>
    </GoogleMapMarker>

    <GoogleMapGeoJSON 
      geojson="https://raw.githubusercontent.com/topobyte/osm4j-examples/master/output/berlin-restaurant-density.geojson"
      :styles="{ fillColor: 'red' }"
    />

    <GoogleMapGeoJSON 
      geojson="https://raw.githubusercontent.com/blackmad/neighborhoods/master/gn-hamburg.geojson"
      :styles="setGeoJSONStyles"
    />
  </GoogleMapLoader>
</template>

<script>
import GoogleMapLoader from "./GoogleMapLoader.vue";
import GoogleMapMarker from "./GoogleMapMarker.vue";
import GoogleMapGeoJSON from "./GoogleMapGeoJSON.vue";

export default {
  components: {
    GoogleMapLoader,
    GoogleMapMarker,
    GoogleMapGeoJSON
  },

  data () {
    return {
      markers: [
        { id: 'Kulturbrauerei', position: { lat: 52.538203, lng: 13.4105247 } },
        { id: 'Wasserturm', position: { lat: 52.5342728, lng: 13.4143335 } }
      ]
    }
  },

  methods: {
    setGeoJSONStyles () {
      return {
        fillColor: Math.random() < 0.5 ? 'red' : 'blue',
      };
    }
  },

  computed: {
    mapConfig () {
      return {
        zoom: 6,
        center: this.mapCenter
      }
    },

    mapCenter () {
      return this.markers[1].position
    }
  },
}
</script>

<style scoped>
.marker {
  width: 4px;
  height: 4px;
  background: red;
  border-radius: 50%;
}
</style>