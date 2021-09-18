<template>
  <div>
    <slot></slot>
  </div>
</template>
<script>
export default {
  inject: ['loader'],

  props: {
    marker: {
      type: Object,
      required: true
    }
  },

  mounted() {
    const { OverlayView, LatLng } = this.loader.google.maps
    class HTMLMarker extends OverlayView {
      constructor({ map, position, element }) {
        super();
        this.latlng = position;
        this.element = element;
        this.setMap(map);
      }
      
      draw() {
        this.element.style.position = 'absolute';

        const panes = this.getPanes();
        panes.overlayImage.appendChild(this.element);    
        
        const latLng = new LatLng(this.latlng.lat, this.latlng.lng)
        const point = this.getProjection().fromLatLngToDivPixel(latLng);
        if (point) {
          this.element.style.left = `${point.x}px`;
          this.element.style.top = `${point.y}px`;
        }
      }

        getPosition() {
          return this.latlng;
        }

        getDraggable() {
          return false;
        }
    }

    new HTMLMarker({
      position: this.marker.position,
      map: this.loader.map,
      element: this.$el
    })

  }
}
</script>