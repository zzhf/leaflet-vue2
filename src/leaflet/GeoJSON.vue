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
    mixins: [mixin],
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
      data(val, oldVal) {
        this.leaflet.addData(val);
      },
      style(val, oldVal) {
        this.resetStyle(val);
      }
    }
  }
</script>