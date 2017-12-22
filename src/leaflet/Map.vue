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
const props = {
  center: {
    type: [Array, Object],
    default: () => [0, 0]
  },
  zoom: {
    type: Number,
    default: 0
  },
  zoomAround: {
    type: Object,
    default: () => {},
    except: true
  },
  zoomPanOptions: {
    type: Object,
    default: () => {},
    except: true
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
  props: {
    ...props
  },
  mixins: [mixin],
  mounted() {
    let mapOptions = this.mixinPropOption(this._props, props);
    //map Object
    this.leaflet = L.map(this.$el, mapOptions);
    this.addEventHook(this.leaflet, events);
    for (let children of this.$children) {
      children._initHooks(this.leaflet);
    }
    console.log(this.leaflet);
  },
  watch: {
    center(val, newVal) {
      this.leaflet.setView(val, null, this.getZoomPanelOption());
    },
    zoom(val, newVal) {
      this.leaflet.setZoom(val, this.getZoomPanelOption());
    },
    minZoom(val, newVal) {
      this.leaflet.setMinZoom(val);
    },
    maxZoom(val, newVal) {
      this.leaflet.setMaxZoom(val);
    },
    crs(val, newVal) {
      console.warn('sorry it`s not available for now!');
    },
    zoomAround(val, newVal) {
      this.leaflet.setZoomAround(val, null, this.options.animate)
    }
  },
  methods: {
    getZoomPanelOption() {
      const zoomPanOptions = this.zoomPanOptions || {
        animate: this.options.animate,
        duration: this.options.duration,
        easeLinearity: this.options.easeLinearity,
        noMoveStart: this.options.noMoveStart
      };
    }
  }
}
</script>

<style>
  .l-map {
    width: 100%;
    height: 100%;
  }
</style>