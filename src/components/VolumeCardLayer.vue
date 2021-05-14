<script>
export default {
  name: "VolumeCardLayer",

  props: {
    width: {
      type: Number,
      default: 360,
    },
    height: {
      type: Number,
      default: 640,
    },
    src: {
      type: String,
      required: true,
    },
    elevation: {
      type: Number,
      default: 0,
    },
  },

  computed: {
    transform() {
      if (this.elevation) {
        return `translateZ(${this.elevation * 10}px)`;
      } else {
        return {};
      }
    },
  },
};
</script>

<template>
  <img
    :src="require(`@/assets${src}`)"
    alt=""
    :width="width"
    :height="height"
    class="volumeCardLayer"
    :style="{ transform }"
  >
</template>

<style lang="scss" scoped>
.volumeCardLayer {
  pointer-events: none;
}
</style>