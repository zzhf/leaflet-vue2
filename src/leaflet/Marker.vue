<template>
    <div>
      <slot></slot>
    </div>
</template>

<script>
  /**
   * http://leafletjs.com/reference-1.2.0.html#marker
   */
  import L from 'leaflet'

  const events = [
    'move',
    'dragstart',
    'movestart',
    'drag',
    'dragend',
    'moveend',
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
    'tooltipclose',
  ];

  export default {
    props: {
      latLng: {
        type: [Object, Array],
        default: () => [0, 0]
      },
      icon: {
        type: Object,
        default: () => new L.Icon.Default()
      },
      draggable: {
        type: Boolean,
        default: false
      },
      title: {
        type: String,
        default: ''
      },
      alt: {
        type: String,
        default: ''
      },
      zIndexOffset: {
        type: Number,
        default: 0
      },
      opacity: {
        type: Number,
        default: 1.0
      },
      riseOnHover: {
        type: Boolean,
        default: false
      },
      riseOffset: {
        type: Number,
        default: 250
      },
      pane: {
        type: String,
        default: 'markerPanel'
      },
      bubblingMouseEvents: {
        type: Boolean,
        defalut: false
      },
      interactive: {
        type: Boolean,
        default: true
      },
      attribution: {
        type: String,
        default: null
      },
      opitons: {
        type: Object,
        default: () => {}
      }
    },
    watch: {
      latLng: {
        handler(val, oldVal) {
          this.leaflet.setLatLng(val)
        },
        deep: true
      }
    },
    mounted() {
      this.leaflet = L.marker(this.latLng, this.options);

      this.leaflet.on('click', function() {
        
      })

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHook(this.$parent.leaflet);
      }
    },
    beforeDestroy() {
      let parent = this.$parent.leaflet;
      if (parent) {
        parent.removeLayer(this.leaflet);
      }
    },
    methods: {
      _initHook(parent) {
        this.leaflet.addTo(parent);
      }
    }
  }
</script>