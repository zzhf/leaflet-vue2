<template>
  
</template>

<script>
  import L from 'leaflet'
  import mixin from './../mixins/mixin'

  const events = [
    'loading',
    'tileunload',
    'tileloadstart',
    'tileerror',
    'tileload',
    'load',
    'add',
    'remove',
    'popupopen',
    'popupclose',
    'tooltipopen',
    'tooltipclose'
  ]

  const props = {
    opacity: {
      type: Number,
      default: 1
    },
    crs: {
      type: Object,
      default: null
    },
    zIndex: {
      type: Number,
    },
    options: {
      type: Object,
      default: () => {}
    }
  }

  export default {
    mixins: [mixin],
    props: {
      ...props,
      url: {
        type: String,
        default: '',
        required: true
      },
    },
    mounted() {
      let layerOptions = this.mixinPropOption(this._props, props);
      this.leaflet = L.supermap.wmtsLayer(this.url, layerOptions);
      this.addEventHook(this.leaflet, events);
      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    watch: {
      url(val, newVal) {
        this.leaflet.setUrl(val);
      },
      opacity(val, newVal) {
        this.leaflet.setOpacity(val);
      },
      zIndex(val, newVal) {
        this.leafelt.setZIndex(val);
      }
    },
    beforeDestroy() {
      let parent = this.$parent.leaflet;
      if (parent) {
        parent.removeLayer(this.leaflet);
      }
    },
    methods: {
      _initHooks(parent) {
        this.leaflet.addTo(parent);
      }
    }
  }
</script>