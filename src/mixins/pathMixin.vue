<template>
  
</template>

<script>
  import L from 'leaflet'
  import mixin from './mixin'

  const props = {
    stroke: {
      type: Boolean,
    },
    color: {
      wight: String,
    },
    weight: {
      type: Number,
    },
    opacity: {
      type: Number
    },
    lineCap: {
      type: String
    },
    lineJoin: {
      type: String
    },
    dashArray: {
      type: String
    },
    dashOffset: {
      type: String
    },
    fill: {
      type: Boolean
    },
    fillColor: {
      type: String
    },
    fillOpacity: {
      type: Number
    },
    fillRule: {
      type: String
    },
    bubblingMouseEvents: {
      type: Boolean
    },
    renderer: {
      type: Object
    },
    className: {
      type: String
    },
    interactive: {
      type: Boolean
    },
    pane: {
      type: Boolean
    },
    attribution: {
      type: String
    }
  }

  export default {
    mixins: [mixin],
    props: {
      ...props,
      options: {
        type: Object,
        default: () => {}
      },
    },
    watch: {
      stroke(val, newVal) {
        this.leaflet.setStyle({ stroke: val });
      },
      color(val, newVal) {
        this.leaflet.setStyle({ color: val });
      },
      weight(val, newVal) {
        this.leaflet.setStyle({ weight: val });
      },
      opacity(val, newVal) {
        this.leaflet.setStyle({ opacity: val });
      },
      lineCap(val, newVal) {
        this.leaflet.setStyle({ lineCap: val });
      },
      lineJoin(val, newVal) {
        this.leaflet.setStyle({ lineJoin: val });
      },
      dashArray(val, newVal) {
        this.leaflet.setStyle({ dashArray: val });
      },
      dashOffset(val, newVal) {
        this.leaflet.setStyle({ dashOffset: val });
      },
      fill(val, newVal) {
        this.leaflet.setStyle({ fill: val });
      },
      fillColor(val, newVal) {
        this.leaflet.setStyle({ fillColor: val });
      },
      fillOpacity(val, newVal) {
        this.leaflet.setStyle({ fillOpacity: val });
      },
      fillRule(val, newVal) {
        this.leaflet.setStyle({ fillRule: val });
      },
    }
  }
</script>