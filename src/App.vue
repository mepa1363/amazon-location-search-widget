<template>
  <div id="map"></div>
</template>

<script setup>
import maplibregl from "maplibre-gl";
import { createMap, createAmplifyGeocoder } from "maplibre-gl-js-amplify";
import markerIcon from "./assets/MarkerIcon.svg";

async function initializeMap() {
  const map = await createMap({
    container: "map",
    center: [-114.067375, 51.046333],
    zoom: 15,
    hash: true,
  });

  map.addControl(new maplibregl.NavigationControl(), "bottom-right");

  const icon = new Image(35, 35);
  icon.src = markerIcon;

  map.addControl(
    createAmplifyGeocoder({
      autocomplete: true,
      countries: "CAN",
      language: "en",
      marker: { element: icon },
      showResultMarkers: { element: icon },
      popup: { offset: 20 },
    }),
    "top-left"
  );
}

initializeMap();
</script>

<style>
@import "maplibre-gl/dist/maplibre-gl.css";
@import "@maplibre/maplibre-gl-geocoder/dist/maplibre-gl-geocoder.css";

body {
  margin: 0;
  padding: 0;
}
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
*:focus {
  outline: none !important;
}
.maplibregl-ctrl-top-left .maplibregl-ctrl {
  width: 400px !important;
  border-radius: 10px;
}
.suggestions {
  border-radius: 10px !important;
}
.maplibregl-ctrl-geocoder--input {
  height: 50px;
  padding: 0px 50px;
}
.maplibregl-ctrl-geocoder--icon-search {
  left: 15px;
  width: 25px;
  height: 35px;
}
.maplibregl-ctrl-geocoder--button {
  right: 15px !important;
  top: 15px !important;
}
.maplibregl-ctrl-geocoder--icon-loading {
  width: 25px;
  height: 25px;
  right: 15px !important;
  top: 15px !important;
}
</style>
