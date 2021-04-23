<script>
export default {
  name: "VolumeCard",

  props: {
    width: {
      type: String,
      default: "540px",
    },
    height: {
      type: String,
      default: "960px",
    },
  },

  data: () => ({
    top: 0,
    left: 0,
    angle: 20,
    transformed: false,
  }),

  computed: {
    transform() {
      return `rotate3d(${this.left}, ${this.top}, 0, ${this.angle}deg)`;
    },
  },

  methods: {
    setCursorCoords(event) {
      this.top = event.y < this.$el.clientHeight / 2 ? "1" : "-1";
      this.left = event.x < this.$el.clientWidth / 2 ? "-1" : "1";
    },
  },
};
</script>

<template>
  <figure
    class="volumeCard"
    @mousemove="setCursorCoords"
    @mouseenter="transformed = true"
    @mouseleave="transformed = null"
    :style="{ width, height }"
  >
    <slot name="background"></slot>
    <div
      class="inner"
      :style="{ transform: transformed && transform, width, height }"
    >
      <slot name="default"></slot>
    </div>
    <figcaption>
      <slot name="caption"></slot>
    </figcaption>
  </figure>
</template>

<style lang="scss" scoped>
.volumeCard {
  position: relative;
  .inner {
    transform-style: preserve-3d;
    transition: transform 1s;
  }

  ::v-deep .volumeCardLayer {
    position: absolute;
    top: 0;
    left: 0;
  }
}
</style>