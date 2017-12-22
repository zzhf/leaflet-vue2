<template>
  <div class="map">
    <l-map :maxZoom="18" :center="[0, 0]" :zoom="5" :crs="crs" :options="mapOptions">
      <l-wms-tilelayer 
        url="http://support.supermap.com.cn:8090/iserver/services/map-china400/wms111/China" 
        :options="wmsOptions">
      </l-wms-tilelayer>
      <!-- <l-sm-wmtslayer 
        url="http://support.supermap.com.cn:8090/iserver/services/map-china400/wmts100" 
        :options="wmtsOptions">
      </l-sm-wmtslayer>
      <l-sm-restlayer url="http://support.supermap.com.cn:8090/iserver/services/map-china400/rest/maps/China">
      </l-sm-restlayer> -->
      <!-- <l-marker :center="[30, 110]"></l-marker> -->
    </l-map>
  </div>
</template>

<script>
  import L from 'leaflet'
  import './../static/lib/iclient9-leaflet'
  import LMap from './leaflet/Map'
  import LMarker from './leaflet/Marker'
  import LWmsTilelayer from './leaflet/WMSTileLayer'
  import LSmWmtslayer from './supermap/WMTSTileLayer'
  import LSmRestlayer from './supermap/RESTTileLayer'

  var res = [];
  for (var i = 0; i < 22; i++) {
    res.push(165664.43905455674 / (Math.pow(2, i)));
  }
  let crs = new L.Proj.CRS("EPSG:3857", {
    origin: [-2.0037508342789244E7, 2.0037508342789244E7],
    resolutions: res,
    bounds: L.bounds([-2.0037508342789244E7, -2.0037508342789244E7], [2.0037508342789244E7, 2.0037508342789244E7])
  })

  export default {
    components: {
      LMap, LMarker, LWmsTilelayer, LSmWmtslayer, LSmRestlayer
    },
    data() {
      return {
        crs: null,
        wmtsOptions: {
            layer: "China",
            style: "default",
            tilematrixSet: "Custom_China",
            format: "image/png",
        },
        wmsOptions: {
          layers: 'China',
          format: 'image/png',
          transparent: true,
          noWrap: true,
        },
        mapOptions: {
          zoom: 0,
          center: [0, 0]
        },
        zoom: 5,
        center: [0, 0]
      }
    }
  }

</script>

<style>
  @import url(./../static/leaflet.css);
  @import url(./../static/lib/iclient9-leaflet.css);

  .map {
    width: 100%;
    height: 600px;
  }
</style>