<template>
  <div class="AppSlider">
    <div
      :style="{ paddingBottom: `${aspectRatio}%` }"
      class="AppSlider__slides"
      @mouseenter="paused = true"
      @mouseleave="paused = false"
    >
      <img
        v-for="(image, index) in images"
        v-show="activeIndex === index"
        :key="index"
        :src="image"
        class="AppSlider__image"
        alt=""
      >
    </div>
    <div class="AppSlider__controls">
      <button
        class="AppSlider__control"
        @click="prev"
      >
        &laquo; prev
      </button>
      <button
        class="AppSlider__control"
        @click="next"
      >
        next &raquo;
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: `AppSlider`,
  props: {
    height: {
      default: 600,
      type: Number,
    },
    images: {
      default: () => [],
      type: Array,
    },
    interval: {
      default: 2000,
      type: Number,
    },
    width: {
      default: 1280,
      type: Number,
    },
  },
  data() {
    return {
      activeIndex: 0,
      paused: false,
      time: this.interval,
    };
  },
  computed: {
    aspectRatio() {
      return (this.height / this.width) * 100;
    },
  },
  created() {
    this.startInterval();
  },
  methods: {
    goToIndex(index) {
      this.activeIndex = index;
      this.time = this.interval;
    },
    next() {
      let nextIndex = this.activeIndex + 1;

      // Go to the first image if the active
      // image ist the last one.
      if (!this.images[nextIndex]) {
        nextIndex = 0;
      }

      this.goToIndex(nextIndex);
    },
    prev() {
      let nextIndex = this.activeIndex - 1;

      // Go to the last image if the active
      // image is the first one.
      if (!this.images[nextIndex]) {
        nextIndex = this.images.length - 1;
      }

      this.goToIndex(nextIndex);
    },
    startInterval() {
      const precision = 100;
      const clock = setInterval(() => {
        if (!this.paused) this.time -= precision;
        if (this.time <= 0) this.next();
      }, precision);

      // Clear the interval if the component
      // is destroyed to prevent memory leaks.
      this.$once(`hook:destroyed`, () => clearInterval(clock));
    },
  },
};
</script>

<style lang="scss">
.AppSlider {
  &__slides {
    position: relative;
  }

  &__image {
    position: absolute;
    width: 100%;
  }

  &__controls {
    display: flex;
    justify-content: space-between;
  }

  // 1. Reset native button styles.
  &__control {
    padding: 0; // 1
    border: none; // 1
    background-color: transparent; // 1
    font-size: 1.25em;
  }
}
</style>
