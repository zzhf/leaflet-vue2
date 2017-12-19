<template>
  <div class="l-map">
    <slot></slot>
  </div>
</template>

<script>
import L from 'leaflet'

/**
 * leaflet map events Array.For details, please look up http://leafletjs.com/reference-1.2.0.html#map-event
 * @type {Array}
 */
const events = [
  //layer events
  'baselayerchange',
  'overlayadd',
  'overlayremove',
  'layeradd',
  'layerremove',
  //Map state change events
  'zoomlevelschange',
  'resize',
  'unload',
  'viewreset',
  'load',
  'zoomstart',
  'movestart',
  'zoom',
  'move',
  'zoomend',
  'moveend',
  //Popup events
  'popupopen',
  'popupclose',
  'autopanstart',
  //Tooltip events
  'tooltipopen',
  'tooltipclose',
  //Location events
  'locationerror',
  'locationfound',
  //Interaction events
  'click',
  'dblclick',
  'mousedown',
  'mouseup',
  'mouseover',
  'mouseout',
  'mousemove',
  'contextmenu',
  'keypress',
  'preclick',
  //animation events
  'zoomanim'
]

/**
 * providing instrictions for common attributes, For more map options details 
 * please look up http://leafletjs.com/reference-1.2.0.html#map-option
 * @type {Object}
 */
const commandOptions = {
  center: {
    type: [Array, Object],
    default: undefined
  },
  zoom: {
    type: [Number],
    default: undefined
  },
  minZoom: {
    type: Number,
    default: *
  },
  maxZoom: {
    type: Number,
    default: *
  },
  maxBounds: {
    type: [Array, Object],
    default: null
  },
  options: {
    type: Object,
    default() => {}
  }
}

export default {
  props: commandOptions,
  mounted() {
    const mapOptions = this.options;
    this.center && mapOptions.center = this.center;
    this.zoom && mapOptions.zoom = this.zoom;
    this.minZoom && mapOptions.minZoom = this.minZoom;
    this.maxZoom && mapOptions.maxZoom = this.maxZoom;
    this.maxBounds && mapOptions.maxBounds = this.maxBounds;
    //map Object
    this.map = L.map(this.$el, mapOptions);
  },
  watch: {
    center(val, oldVal) {
      this.map.
    },
    zoom(val, oldVal) {

    },
    minZoom(val, oldVal) {

    },
    maxZoom(val, oldVal) {

    },
    maxBounds(val, oldVal) {

    },
    options: {
      handler(val, oldVal) {

      },
      deep: true
    }
  },
  methods: {

  }
}
</script>