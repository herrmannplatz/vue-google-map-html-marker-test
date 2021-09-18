<template>
  <GoogleMapLoader
    class="relative"
    :mapConfig="mapConfig"
    :apiKey="apiKey"
  >
    <GoogleMapSearchBox class="absolute top-14 left-4"/>

    <GoogleMapMarker
      v-for="marker in markers"
      :key="marker.id"
      :marker="marker"
    >
      <div class="w-4 h-4 rounded-full bg-red-600"></div>
    </GoogleMapMarker>

    <GoogleMapGeoJSON 
      geojson="https://raw.githubusercontent.com/topobyte/osm4j-examples/master/output/berlin-restaurant-density.geojson"
      :styles="mapStyles"
    />

    <!-- <GoogleMapGeoJSON 
      geojson="https://raw.githubusercontent.com/blackmad/neighborhoods/master/gn-hamburg.geojson"
      :styles="setGeoJSONStyles"
    /> -->
  </GoogleMapLoader>
</template>

<script>
import GoogleMapLoader from "./GoogleMapLoader.vue";
import GoogleMapMarker from "./GoogleMapMarker.vue";
import GoogleMapGeoJSON from "./GoogleMapGeoJSON.vue";
import GoogleMapSearchBox from "./GoogleMapAutocomplete.vue";

export default {
  components: {
    GoogleMapLoader,
    GoogleMapMarker,
    GoogleMapGeoJSON,
    GoogleMapSearchBox
  },

  data () {
    return {
      apiKey: process.env.VUE_APP_GOOGLE_API_KEY,
      mapStyles: { fillColor: 'red' },
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

  mounted () {
    setTimeout(() => {
      this.mapStyles.fillColor = 'blue'
    }, 5000)
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