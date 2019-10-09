<template>
  <div id="mapid">
    <RandoFilter />
  </div>
</template>

<script>
// a la place de hikings -> running
import runnings from '../static/running.js'
import * as L from 'leaflet'
import RandoFilter from '~/components/RandoFilter.vue'
// import 'leaflet-routing-machine'
function createMap() {
  //the point of launching page
  var mymap = L.map('mapid').setView([43.295336, 5.373907], 15)

  L.tileLayer(
    'https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1Ijoicm9iZXJ0cGV0cnQiLCJhIjoiY2sxaHp2YThkMWYxYzNjcW0zYWx2dWtmeSJ9.FztRaZQJmLRV9fBarMYCIg',
    {
      attribution:
        'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 12,
      id: 'mapbox.streets',
      accessToken: 'your.mapbox.access.token'
    }
  ).addTo(mymap)

  // --- add points on the map --- will be done later to use Robert's icon
  //var marker = L.marker([43.265744, 5.395173]).addTo(mymap);

  //var marker2 = L.marker([43.261088, 5.39804]).addTo(mymap);

  L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}{r}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(mymap)

  // --- change icons ----
  var runningIcon = L.icon({
    iconUrl: require('~/assets/images/running.png'),
    iconSize: [35, 35],
    iconAnchor: [0, 0],
    popupAnchor: [0, 0],
    shadowSize: [0, 0],
    shadowAnchor: [0, 0]
  })
  // le console log fonction pour
  // console.log(hikings['kml']['Document']['Folder']['Placemark'][0]['Point'][
  //         'coordinates'
  //       ].split(',')[1])
  // console.log(hikings['kml']['Document']['Folder'])

  runnings.forEach(function(running) {
    const mapMarker = L.marker(
      [running['coordinates']['latitude'], running['coordinates']['longitude']],
      {
        icon: runningIcon
      }
    ).addTo(mymap)
    mapMarker.bindPopup(
      '<strong>' +
        running['name'] +
        '</strong><p>' +
        running['description'] +
        '</p>'
    )
    // .openPopup()
  })
}
export default {
  components: {
    RandoFilter
  },
  mounted() {
    createMap()
  }
}
</script>

<style>
#mapid {
  height: 100vh;
  width: 100vw;
}

div.line-mouse-marker {
  background-color: #ffffff;
  border: 2px solid black;
  border-radius: 10px;
}
.leaflet-bar {
  display: none;
}
</style>
