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
    return {
      places: [
        { lat: -81.850513, lng: 28.808834, description: "My home in Florida!" },
        { lat: 55.203738, lng: 131.3855, description: "My home in Alaska!" },
        { lat: 41.906326, lng: -87.683779, description: "My home in Chicago!" },
      ],
    };
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
        style: "mapbox://styles/mapbox/streets-v11", // style URL
        center: [-104.9, 39.5], // starting position [lng, lat]
        zoom: 9, // starting zoom
        projection: "globe", // display the map as a 3D globe
      });

      // create the popup
      const popup = new mapboxgl.Popup({ offset: 25 }).setText("This is a pop up to tell you a thing about a place.");

      // Create a default Marker and add it to the map.
      const marker1 = new mapboxgl.Marker().setLngLat([-104.9, 39.5]).setPopup(popup).addTo(map);

      const marker3 = new mapboxgl.Marker().setLngLat([-81.850513, 28.808834]).setPopup(popup).addTo(map);

      // Create a default Marker, colored black, rotated 90 degrees.
      const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 }).setLngLat([-104.9, 39.5]).addTo(map);

      map.on("style.load", () => {
        map.setFog({}); // Set the default atmosphere style
      });
      console.log(marker1, marker2, marker3, popup);
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
  height: 500px;
  width: 500px;
  margin-left: 25px;
}
</style>
