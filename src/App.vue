<template>
  <div id="app">
    <app-slider
      :images="[
        `https://res.cloudinary.com/maoberlehner/image/upload/c_thumb,f_auto,g_center,w_1280,h_600/v1532772050/blog/demos/ken-burns-slider/1.jpg`,
        `https://res.cloudinary.com/maoberlehner/image/upload/c_thumb,f_auto,g_center,w_1280,h_600/v1532772050/blog/demos/ken-burns-slider/2.jpg`,
        `https://res.cloudinary.com/maoberlehner/image/upload/c_thumb,f_auto,g_center,w_1280,h_600/v1532772050/blog/demos/ken-burns-slider/3.jpg`,
        `https://res.cloudinary.com/maoberlehner/image/upload/c_thumb,f_auto,g_center,w_1280,h_600/v1532772050/blog/demos/ken-burns-slider/4.jpg`,
      ]"
    />
  </div>
</template>

<script>
import AppSlider from './components/AppSlider.vue';

export default {
  name: `App`,
  components: {
    AppSlider,
  },
};
</script>

<style lang="scss">
@import './assets/scss/generic/base';
</style>
