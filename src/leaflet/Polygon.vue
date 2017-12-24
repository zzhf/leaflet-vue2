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
    smoothFactor: {
      type: Number,
    },
    noClip: {
      type: Boolean,
    },
    interactive: {
      type: Boolean,
      default: true
    },
    pane: {
      type: String,
    },
    attribution: {
      type: String
    }
    options: {
      type: Object,
      default: () => {}
    },
  }
 
  export default {
    mixins: [pathMixin],
    props: {
      ...props,
      latLngs: {
        type: Array
      }
    },

    mounted() {
      let layerOptions = this.mixinPropOption(this._props, props);

      this.leaflet = L.polygon(this.latlngs, layerOptions);

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
    },
    beforeDestroy() {
      let parent = this.$parent.leaflet;
      if (parent) {
        parent.removeLayer(this.leaflet);
      }
    }
  }
</script>