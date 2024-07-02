<template>
  <div>
    <base-header class="pb-6">
      <b-row align-v="center" class="py-4">
        <b-col lg="6" cols="7" >
          <h6 class="h2 text-white d-inline-block mb-0">{{$route.name}}</h6>
          <nav aria-label="breadcrumb" class="d-none d-md-inline-block ml-md-4">
            <route-breadcrumb/>
          </nav>
        </b-col>
        <b-col lg="6" cols="5" class="text-right">
          <base-button size="sm" type="neutral">New</base-button>
          <base-button size="sm" type="neutral">Filters</base-button>
        </b-col>
      </b-row>
    </base-header>

    <b-container fluid class="mt--6">
      <b-row>
        <b-col>
          <b-card no-body class="border-0">
            <div id="map" class="map-canvas"
                 style="height: 600px;"></div>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
import { Loader } from "@googlemaps/js-api-loader";
const loader = new Loader({ apiKey: "YOUR_API_KEY" });

  export default {
    mounted() {
      loader.load().then(function () {
        // Regular Map
        const myLatlng = new google.maps.LatLng(40.748817, -73.985428);
        const mapOptions = {
          zoom: 13,
          center: myLatlng,
          scrollwheel: false, // we disable de scroll over the map, it is a really annoing when you scroll through page
          disableDefaultUI: true, // a way to quickly hide all controls
          zoomControl: true,
          styles: [
            {
              featureType: "administrative",
              elementType: "labels.text.fill",
              stylers: [{ color: "#444444" }],
            },
            {
              featureType: "landscape",
              elementType: "all",
              stylers: [{ color: "#f2f2f2" }],
            },
            {
              featureType: "poi",
              elementType: "all",
              stylers: [{ visibility: "off" }],
            },
            {
              featureType: "road",
              elementType: "all",
              stylers: [{ saturation: -100 }, { lightness: 45 }],
            },
            {
              featureType: "road.highway",
              elementType: "all",
              stylers: [{ visibility: "simplified" }],
            },
            {
              featureType: "road.arterial",
              elementType: "labels.icon",
              stylers: [{ visibility: "off" }],
            },
            {
              featureType: "transit",
              elementType: "all",
              stylers: [{ visibility: "off" }],
            },
            {
              featureType: "water",
              elementType: "all",
              stylers: [{ color: "#5e72e4" }, { visibility: "on" }],
            },
          ],
        };
        const map = new google.maps.Map(
          document.getElementById("map"),
          mapOptions
        );
        const marker = new google.maps.Marker({
          position: myLatlng,
          title: "Regular Map!",
        });
        marker.setMap(map);
      });
    },
  };
</script>
