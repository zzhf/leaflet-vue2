<template>
  <div class="l-map">
    <slot></slot>
  </div>
</template>

<script>
import L from 'leaflet'
import mixin from './../mixins/mixin'

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
    default: () => [0, 0]
  },
  zoom: {
    type: [Number],
    default: undefined
  },
  zoomPanOptions: {
    type: Object,
    default: () => {}
  },
  minZoom: {
    type: Number,
  },
  maxZoom: {
    type: Number,
  },
  maxBounds: {
    type: [Array, Object],
    default: null
  },
  crs: {
    type: Object,
  },
  options: {
    type: Object,
    default: () => {}
  }
}

export default {
  props: commandOptions,
  mixins: [mixin],
  mounted() {
    let mapOptions = Object.assign({},this.options);

    // console.log(this.center);
    if (this.center) {
      mapOptions.center = this.center;
    }
    if (this.zoom) {
      mapOptions.zoom = this.zoom;
    }
    if (this.minZoom) {
      mapOptions.minZoom = this.minZoom;
    }
    if (this.maxZoom) {
      mapOptions.maxZoom = this.maxZoom;
    }
    if (this.maxBounds) {
      mapOptions.maxBounds = this.maxBounds;
    }
    if (this.crs) {
      mapOptions.crs = this.crs
    }
    //map Object
    this.leaflet = L.map(this.$el, mapOptions);
    this.addEventHook(this.leaflet, events);
    console.log(this);
    for (let children of this.$children) {
      children._initHooks(this.leaflet);
    }
  },
  watch: {
    // center(val, oldVal) {
    //   this.leaflet.setView(val, this.zoomPanOptions);
    // },
    // zoom(val, oldVal) {
    //   this.leaflet.setView(zoom, this.zoomPanOptions);
    // },
    // minZoom(val, oldVal) {
    //   this.leaflet.setMinZoom(val);
    // },
    // maxZoom(val, oldVal) {
    //   this.leaflet.setMaxZoom(val);
    // },
    // maxBounds(val, oldVal) {
    //   this.leaflet.maxBounds(val);
    // },
    // options: {
    //   handler(val, oldVal) {
    //     L.setOptions(this.leaflet, val);
    //   },
    //   deep: true
    // }
  },
  methods: {
    invalidateSize(animate) {
      this.map.invalidateSize(animate);
    }
  }
}
</script>