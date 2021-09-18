<template>
  <div></div>
</template>

<script>
export default {
  inject: ['loader'],

  data () {
    return {
      dataLayer: null
    }
  },

  props: {
    geojson: {
      type: [Object, String],
      required: true
    },
    styles: {
      type: [Function, Object],
    }
  },

  methods: {
    getDataLayer () {
      if (!this.dataLayer) {
        this.dataLayer = new this.loader.google.maps.Data({ map: this.loader.map })
      }
      return this.dataLayer
    }
  },

  watch: {
    geojson: {
      handler(value) {
        this.getDataLayer().loadGeoJson(value)
      },
      immediate: true,
      deep: true
    },
    styles: {
      handler(value) {
        this.getDataLayer().setStyle(value)
      },
      immediate: true,
      deep: true
    },
  },

  destroyed () {
    this.dataLayer.forEach((feature) => {
      this.dataLayer.remove(feature);
    })
    this.dataLayer = null
  }
}
</script>