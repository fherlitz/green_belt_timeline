<template>
  <!-- Navigation Bar -->
  <header class="text-center py-4 bg-success text-light">
    <h1 style="font-size: 40px;">Green Belt Timeline</h1>
    <h6>Vizualizing Urban Growth Over Time</h6>
  </header>

  <!-- Main Content -->
  <div class="container my-5" style="max-width: 900px; width: 90%">
    <h2>What is the <a class="text-success text-decoration-none">Green Belt</a> in England?</h2>
    <br>
    <h6>
      The Green Belt in England is an <strong>urban planning strategy</strong> to limit the uncontrolled expansion of cities and to preserve open landscapes around urban areas. The purpose of this <a class="text-success" href="https://assets.publishing.service.gov.uk/media/675abd214cbda57cacd3476e/NPPF-December-2024.pdf">policy</a> is to prevent urban sprawl, protect natural areas, agricultural land and promote the use of existing built-up areas. In the following map one can see if this policy has been effective in Birmingham and London over the years.
    </h6>
  </div>

  <!-- Slider -->
  <Slider @changeYears="loadGeoJson"></Slider>
    
  <!-- Map -->
  <div class="container my-4">
    <main class="shadow">
      <l-map ref="map" v-model:zoom="zoom" v-model:center="center" :useGlobalLeaflet="false">
        <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
                      layer-type="base"
                      name="Openstreetmap Basemap">
        </l-tile-layer>
        <l-geo-json :geojson="geojsonL"></l-geo-json>
        <l-geo-json :geojson="geojsonB"></l-geo-json>
      </l-map>
    </main>
  </div>

  <!-- Plots & Paragraph -->
  <div class="container my-5" style="max-width: 900px; width: 90%">
    <h2 class="text-center mb-4"><a class="text-success text-decoration-none">Green Belt</a> Area over the Years</h2>
    <Plots
      :londonImg="londonPlot"
      :birminghamImg="birminghamPlot"
    ></Plots>
    <h4 class="text-success">Urban Development Pressure</h4>
    <br>
    <h6>
      The significant reduction in Green Belt areas around London and Birmingham since 2018 is primarily due to <strong>urban development pressures</strong> of housing shortages, population growth and significant policy adjustments. The <strong>demand for housing</strong> in these expanding cities needed the development of new residential areas to provide housing and accommodate the growing population, often interfering with protected Green Belt zones.
    </h6>
    <br>
    <h6>
      <strong>Policy changes</strong>, especially updates to the <a class="text-success" href="https://assets.publishing.service.gov.uk/media/675abd214cbda57cacd3476e/NPPF-December-2024.pdf">National Planning Policy Framework (NPPF)</a>, have introduced more flexible planning policies that allow development within green belts under certain conditions. The effects of this development pressure result in <strong>environmental degradation and loss of biodiversity</strong>, which has a negative impact on the ecology of England. 
    </h6>
    <br>
    <h6>
      Balancing the need for urban growth with the preservation of the green belt requires strategic planning and a robust policy framework. Through a balanced and sustainable approach, it is possible to meet the demands of urban growth without compromising the boundaries of the green belt.
    </h6>
  </div>

  <footer class="bg-light d-flex justify-content-center align-items-center p-3 mb-4">
    <img src="/favicon.ico" alt="Favicon" class="mt-2" style="width: 30px; height: 30px;">
  </footer>
</template>

<script>
import "leaflet/dist/leaflet.css"
import { LMap, LTileLayer, LGeoJson } from "@vue-leaflet/vue-leaflet"
import Slider from "./components/Slider.vue";
import Plots from "./components/Plots.vue";
import londonPlot from "@/assets/london.png";
import birminghamPlot from "@/assets/birmingham.png";

export default {
  components: {
    LMap,
    LTileLayer,
    LGeoJson,
    Slider,
    Plots
  },
  data(){
    return {
      // Default values
      zoom:6,
      center: [54, -3],
      londonPlot,
      birminghamPlot,
    }
  },
  created(){
    this.loadGeoJson("2003")
  },
  methods: { // Load GeoJSON data
    loadGeoJson(sliderValue){
      console.log("Changed to ".concat(sliderValue))
      fetch("./src/data/London".concat(sliderValue,".geojson"))
        .then((response) => response.json())
        .then((data) => {
          this.geojsonL = data;
        })
        .catch((error) => {
          console.error("Error loading GeoJSON:", error);
        });

      fetch("./src/data/Birmingham".concat(sliderValue,".geojson"))
        .then((response) => response.json())
        .then((data) => {
          this.geojsonB = data;
        })
        .catch((error) => {
          console.error("Error loading GeoJSON:", error);
        });
    },
  }
}

</script>

<style>
html, body {
  margin: 0;
  padding: 0;
}

main {
  height: 80vh;
  width: 100%;
}

path {
  fill: #2E7D32;
  stroke: #198754;
}
</style>
