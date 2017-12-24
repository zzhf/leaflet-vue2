<template>
  
</template>

<script>
  import L from 'leaflet'
  import pathMixin from './../mixins/pathMixin'

  const events = [
    'click',
    'dblclick',
    'mousedown',
    'mouseover',
    'mouseout',
    'contextmenu',
    'add',
    'remove',
    'popupopen',
    'popupclose',
    'tooltipopen',
    'tooltipclose'
  ]

  const props = {
    interactive: {
      type: Boolean,
      default: true
    },
    pane: {
      type: String,
    },
    attribution: {
      type: String
    },
    options: {
      type: Object,
      default: () => {}
    },
    radius: {
      type: Number
    },
  }
 
  export default {
    mixins: [pathMixin],
    props: {
      ...props,
      center: {
        type: [Array, Object]
      }
    },

    mounted() {
      let layerOptions = this.mixinPropOption(this._props, props);

      this.leaflet = L.circleMarker(this.center, layerOptions);

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    watch: {
      radius(val, newVal) {
        this.leaflet.setRadius(val);
      },
      center(val, newVal) {
        this.leafelt.setLatLng(val);
      },
      smoothFactor(val, newVal) {
        this.leaflet.setSmoothFactor(val);
      },
      noClip(val, newVal) {
        this.leafelt.setNoClip(val);
      }
    },
    beforeDestroy() {
      let parent = this.$parent.leaflet;
      if (parent) {
        parent.removeLayer(this.leaflet);
      }
    }
  }
</script>