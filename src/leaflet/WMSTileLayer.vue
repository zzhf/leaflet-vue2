<template>
	
</template>

<script>
	import L from 'leaflet'
  import mixin from './../mixins/mixin'

  export default {
    mixins: [mixin],
    props: {
      url: {
        type: String,
        default: '',
        required: true
      },
      layers: {
        type: String,
        default: ''
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
      this.wmsOptions = Object.assign({}, this.options);
      // this.layers && this.options.layers = this.layers;
      // this.styles && this.options.styles = this.styles;
      // this.format && this.options.format = this.format;
      // this.transparent && this.options.transparent = this.transparent;
      // this.crs && this.options.crs = this.crs;
      // this.uppercase && this.options.uppercase = this.uppercase;

      this.leaflet = L.tileLayer.wms(this.url, this.wmsOptions);

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
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
        console.log('i was hooks')
        this.leaflet.addTo(parent)
        console.log(parent)
      }
    }    
  }
</script>