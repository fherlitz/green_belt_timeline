<template>
    <div class="container my-4">
      <div class="card p-4 shadow-sm" style="width: 70%; margin: 0 auto;">
        <h2 class="card-title text-center">Select a Year</h2>
        <!-- Slider -->
        <div class="form-group">
          <input 
            type="range" 
            class="form-range" 
            min="1997" 
            max="2024" 
            v-model="sliderValue" 
            step="1" 
            @change="emitChange"
          />
        </div>
        <p class="text-center">Current Year: <strong>{{ sliderValue }}</strong></p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Slider",
    data(){
      return {
        sliderValue: 2003
      }
    },
    methods:{
      // The case years below are the years where the data is unavailable
      emitChange(){ 
        switch(Number(this.sliderValue)){
          case 1998:
          case 1999:
          case 2000:
          case 2001:
          case 2002:
            this.sliderValue = "2003"
            break
          case 2004:
          case 2005:
          case 2006:
            this.sliderValue = "2007"
            break
          case 2008:
          case 2009:
          case 2010:
            this.sliderValue = "2011"
            break
        }
        this.$emit('changeYears', this.sliderValue)
      }
    }
  };
  </script>
 