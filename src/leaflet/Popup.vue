<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  import L from 'leaflet'
  import mixin from './../mixins/mixin'

  const events = [
    'add',
    'remove',
    'popupopen',
    'popupclose',
    'tooltipopen',
    'tooltipclose'
  ]

  const props = {
    latLng: {
      type: [Array, Object]
    },
    maxWidth: {
      type: Number,
    },
    minWidth: {
      type: Number,
    },
    maxHeight: {
      type: Number,
    },
    autoPan: {
      type: Boolean,
    },
    autoPanPaddingTopLeft: {
      type: [Object, Array],
    },
    autoPanPaddingBottomRight: {
      type: [Object, Array],
    },
    autoPanPadding: {
      type: [Object, Array],
    },
    autoPanPadding: {
      type: Boolean,
    },
    closeButton: {
      type: Boolean,
      default: true,
    },
    autoClose: {
      type: Boolean,
      default: true,
    },
    closeOnClick: {
      type: Boolean,
    },
    className: {
      type: String,
    },
    offset: {
      type: [Array, Object],
    },
    pane: {
      type: String,
    },
    attribution: {
      type: String,
    },
    source: {
      type: Object,
      except: true
    },
    options: {
      type: Object,
      default: () => {}
    },
  }

  export default {
    mixins: [mixin],
    props: {
      ...props,
      latLng: {
        type: [Array, Object]
      },
      content: null,
      show: {
        type: Boolean,
        default: true
      }
    },
    mounted() {
      let layerOptions = this.mixinPropOption(this._props, props);

      this.leaflet = L.popup(layerOptions, this.source || null);

      if (this.latLng) {
        this.leaflet.setLatLng(this.latLng);
      }

      //TODO add VNODE support
      if (this.content) {
        this.leaflet.setContent(this.content);
      }

      if (this.show && this.parent._isMounted) {
        this._initHooks(this.$parent);
      }

      this.addEventHook(this.leaflet, events);

      if (this.$parent._isMounted) {
        this._initHooks(this.$parent);
      }
    },
    watch: {
      latLng(val, newVal) {
        this.leaflet.setLatLng(val);
      },
      content(val, newVal) {
        this.leaflet.setContent(val);
      },
      show(val, newVal) {
        if (val && !this.leaflet.isOpen()) {
          let source = this.source || this.$parent.leaflet;
          this.leaflet.openOn(source);
        }else {
          this.leaflet.closePopup()
        }
      }
    },
    beforeDestroy() {
      let parent = this.$parent.leaflet;
      if (parent.getPopup()) {
        parent.unbindPopup();
      }
    },
    methods: {
      _initHooks(parent) {
        let source = this.source || parent;
        source.bindPopup(this.leaflet);
        if (this.show) {
          this.leaflet.openOn(source);
        }
      }
    }
  }
</script>