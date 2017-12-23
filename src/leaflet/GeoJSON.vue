<template>
  
</template>

<script>
  import L from 'leaflet'
  import mixin from './../mixins/mixin'

  const events = [
    'layeradd',
    'layerremove',
    'add',
    'remove',
    'popupopen',
    'popupclose',
    'tooltipopen',
    'tooltipclose'
  ]

  const props = {
    pointToLayer: {
      type: Function
    },
    style: {
      type: Function
    },
    onEachFeature: {
      type: Function
    },
    filter: {
      type: Function
    },
    coordsToLatLng: {
      type: Function
    },
    options: {
      type: Object
    }
  }

  export default {
    mixins: [mixin],
    props: {
      ...props,
      data: {
        type: Object,
        // required: true
      },
    }
    mounted() {
      let geojsonOptions = this.mixinPropOptions(this._props, props);

      this.leaflet = L.GeoJSON(this.data, geojsonOptions)

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    watch: {
      data: {
        handler(val, oldVal) {
          this.leaflet.addData(val);
        }
      },
      style: {
        handler(val, oldVal) {
          this.leaflet.addData(val);
        }
      }
    },
    methods: {
      // _initHooks(parent) {
      //   this.leaflet.addTo(parent)
      // }
    }
  }
</script>