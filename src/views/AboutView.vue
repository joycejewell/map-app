<template>
  <div class="about">
    <h1>This is my map</h1>
    <div id="map"></div>
  </div>
</template>
<script>
/* global mapboxgl */
export default {
  data: function () {
    return {};
  },
  created: function () {}, // runs after JS has loaded
  mounted: function () {
    // runs after DOM(html) is loaded
    this.showMap();
  },
  methods: {
    showMap: function () {
      mapboxgl.accessToken = process.env.VUE_APP_MAP_KEY;
      const map = new mapboxgl.Map({
        container: "map", // container ID
        style: "mapbox://styles/mapbox/dark-v10", // style URL
        center: [-87.623177, 41.881832], // starting position [lng, lat]
        zoom: 9, // starting zoom
        projection: "globe", // display the map as a 3D globe
      });
      map.on("style.load", () => {
        map.setFog({}); // Set the default atmosphere style
      });
    },
  },
};
</script>
<style>
body {
  margin: 0;
  padding: 0;
}
#map {
  height: 300px;
  width: 500px;
  margin-left: 25px;
}
</style>
