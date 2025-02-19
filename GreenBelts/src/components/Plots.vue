<template>
    <div class="container my-5">
      <!-- London Plot -->
      <div class="row justify-content-center">
        <div class="col-md-5 mb-4">
          <img @click="openPlot(londonImg)" :src="londonImg" alt="London" class="img-fluid rounded shadow plot cursor-pointer" />
        </div>
        <!-- Birmingham Plot -->
        <div class="col-md-5 mb-4">
          <img @click="openPlot(birminghamImg)" :src="birminghamImg" alt="Birmingham" class="img-fluid rounded shadow plot cursor-pointer" />
        </div>
      </div>

      <!-- Plot Fullscreen -->
      <div v-if="isPlotOpen" class="plot-overlay" @click="closePlot">
        <div class="plot-content" @click.stop>
          <!-- Display the selected plot -->
          <img :src="selectedImage" alt="Full Screen Plot" class="img-fluid" />
          <!-- Close Button -->
          <button class="close-button" @click="closePlot">&times;</button>
        </div>
      </div>
    </div>
</template>

<script>
export default { // Export the plots for use in the App.vue
  name: "Plots",
  props: {
    londonImg: {
      type: String,
      required: true
    },
    birminghamImg: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      isPlotOpen: false,
      selectedImage: ''
    };
  },
  methods: {
    // Opens the plot and sets the selected image
    openPlot(image) {
      this.selectedImage = image;
      this.isPlotOpen = true;
    },
    // Closes the fullscreen mode
    closePlot() {
      this.isPlotOpen = false;
      this.selectedImage = '';
    }
  }
};
</script>

<style scoped>
.cursor-pointer {
  cursor: pointer;
}

.plot-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; 
}

.plot-content {
  position: relative;
  max-width: 800px;
  max-height: 800px;
  overflow: auto; 
}

.plot-content img {
  width: 100%;
  height: auto;
  border-radius: 8px;
}

.close-button {
  position: absolute;
  top: 0px;
  left: 15px;
  font-size: 40px;
  color: rgb(0, 0, 0);
  background: transparent;
  border: none;
  cursor: pointer;
  outline: none;
}

.plot-overlay {
  animation: fadeIn 0.2s;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>