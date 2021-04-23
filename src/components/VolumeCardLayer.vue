<script>
export default {
  name: "VolumeCardLayer",

  props: {
    width: {
      type: Number,
      default: 540,
    },
    height: {
      type: Number,
      default: 960,
    },
    src: {
      type: String,
      required: true,
    },
    elevation: {
      type: [String, Number],
      default: 0,
    },
  },

  computed: {
    transform() {
      return `translateZ(${
        isNaN(this.elevation) ? this.elevation : this.elevation * 10 + "px"
      })`;
    },
  },
};
</script>

<template>
  <img
    :src="src"
    alt=""
    :width="width"
    :height="height"
    class="volumeCardLayer"
    :style="{ transform }"
  />
</template>

<style lang="scss">
</style>