<template>
  <input
    ref="input"
    type="text"
    placeholder="Search ..."
  />
</template>

<script>
export default {
  inject: ['loader'],

  data () {
    return {
      searchBox: null
    }
  },

  mounted () {
    this.searchBox = new this.loader.google.maps.places.Autocomplete(this.$refs.input);
    this.searchBox.addListener('place_changed', () => {
      this.$emit('place_changed', this.searchBox.getPlace())
    })
  }

}
</script>