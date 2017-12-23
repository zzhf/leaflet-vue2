<template>
  
</template>

<script>
  import L from 'leaflet'
  import mixin from './../mixins/mixin'

  const events = [
    'toGeoJSON',
    'getLatLngs',
    'setLatLngs',
    'isEmpty',
    'getCenter',
    'getBounds',
    'addLatLng'
  ]

//options太多了 自己写吧
  const props = {
    smoothFactor: {
      type: Number,
      default: 1
    },
    noClip: {
      type: Boolean,
    },
    stroke: {
      type: Boolean
    }
    options: {
      type: Object,
      default: () => {}
    },
  }
 
  export default {
    props: {
      latLngs: {
        type: Array
      }
    },

    mounted() {
      let layerOptions = this.mixinPropOption(this._props, props);

      this.leaflet = L.polyline(this.latlngs, layerOptions);

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    watch: {
      latLngs(val, newVal) {
        this.leaflet.setLatLngs(val);
      },
      smoothFactor(val, newVal) {
        this.leaflet.setSmoothFactor(val);
      },
      noClip(val, newVal) {
        this.leafelt.setNoClip(val);
      }
    }
  }
</script>