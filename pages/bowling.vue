<template>
  <div id="mapid">
    <RandoFilter />
  </div>
</template>

<script>
// a la place de hikings -> bowling
import bowlings from '../static/bowling.js'
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

  // --- creating hiking paths ---
  // L.Routing.control({
  //   waypoints: [
  //     L.latLng(43.261088, 5.39804),
  //     L.latLng(43.262, 5.4),
  //     L.latLng(43.261088, 5.39804)
  //   ],
  //   routeWhileDragging: true
  // }).addTo(mymap)

  // L.Routing.control({
  //   waypoints: [
  //     L.latLng(43.301999, 5.36554),
  //     L.latLng(43.331999, 5.39554),
  //     L.latLng(43.381999, 5.30554)
  //   ],
  //   routeWhileDragging: true
  // }).addTo(mymap)

  // --- change icons ----
  var myIcon = L.icon({
    iconUrl: require('~/assets/images/hiking.png'),
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

  bowlings.forEach(function(bowling) {
    const mapMarker = L.marker(
      [bowling['coordinates']['latitude'], bowling['coordinates']['longitude']],
      {
        icon: myIcon
      }
    ).addTo(mymap)
    mapMarker
      .bindPopup(
        '<strong>' +
          bowling['name'] +
          '</strong><p>' +
          bowling['description'] +
          '</p>'
      )
      .openPopup()
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
