<template>
  <div id="container">
    <div id="mapContainer"></div>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  name: "Map",
  data() {
    return {
      center: [-0.789275,113.921327],
      zoom: 5,
      map: null,
    };
  },
  methods: {
    setupLeafletMap () {
      this.map = L.map("mapContainer").setView(this.center, this.zoom);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(this.map)

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaBarat:jabar3',
          transparent: true,
          format: 'image/png'
      }).addTo(this.map);

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaTengah:jateng',
          transparent: true,
          format: 'image/png'
      }).addTo(this.map);

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaTimur:jatim',
          transparent: true,
          format: 'image/png'
      }).addTo(this.map);
    },
  },
  mounted() {
    this.setupLeafletMap();
  },
};
</script>

<style scoped>
#container {
  display: flex;
}
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>