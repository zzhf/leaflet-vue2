<template></template>

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

  export default {
    mixins: [mixin],
    props: {
      url: {
        type: String,
        default: '',
        required: true
      },
      styles: {
        type: String,
        default: ''
      },
      format: {
        type: String,
        default: 'image/png' //override the leaflet default value
      },
      transparent: {
        type: Boolean,
        default: true
      },
      crs: {
        type: Object,
        default: null
      },
      uppercase: {
        type: Boolean,
        default: false
      },
      options: {
        type: Object,
        default: () => {}
      }
    },
    mounted() {
      console.log('i am in')
      this.leaflet = L.supermap.wmtsLayer(this.url, this.options);

      this.addEventHook(this.leaflet, events);
      console.log(this.leaflet);
      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    beforeDestroy() {
      console.log('i was destroy')
      let parent = this.$parent.leaflet;
      if (parent) {
        parent.removeLayer(this.leaflet);
      }
    },
    methods: {
      _initHooks(parent) {
        console.log('i am initHooks')
        this.leaflet.addTo(parent);
      }
    }
  }
</script>