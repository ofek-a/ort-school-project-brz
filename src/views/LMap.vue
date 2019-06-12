<template>
  <div>
    <div id="map"></div>
  </div>
</template>

<script>
export default {
  name: "lmap",
  mounted() {
    this.$nextTick(() => {
      var apiKey = process.env.BRZ_API_KEY; // Your BreezoMeter API key
      var errorMessage =
        "Update the variable 'apiKey' with a BreezoMeter API key to see the tiles. Contact BreezoMeter if you need any help:    breezometer.com/contact-us";

      // Map
      var map = L.map("map", {
        center: [46.227638, 2.213749],
        zoom: 6,
        minZoom: 3
      });

      L.tileLayer(
        "https://{s}.tile.openstreetmap.se/hydda/full/{z}/{x}/{y}.png",
        {
          maxZoom: 18,
          attribution:
            'Tiles courtesy of <a href="http://openstreetmap.se/" target="_blank">OpenStreetMap Sweden</a> &mdash; Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }
      ).addTo(map);

      // Overlay BreezoMeter Layer
      L.tileLayer(
        "https://tiles.breezometer.com/v1/air-quality/breezometer-aqi/current-conditions/{z}/{x}/{y}.png?key=" +
          (apiKey === "" ? alert(errorMessage) : apiKey),
        {
          tms: false,
          opacity: 0.65,
          maxNativeZoom: 8
        }
      ).addTo(map);
    });
  }
};
</script>

<style>
#map {
  position: relative;
  height: 50vh;
}
</style>
