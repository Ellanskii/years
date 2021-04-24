<script>
import { throttle, debounce } from "lodash";

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
    perspective: {
      type: String,
      default: "1000px",
    },
    maxAngle: {
      type: Number,
      default: 45,
    },
  },

  data: () => ({
    rotateX: 0,
    rotateY: 0,
    angle: 20,
    transformed: false,
  }),

  computed: {
    transform() {
      return `rotate3d(${this.rotateX}, ${this.rotateY}, 0, ${this.angle}deg)`;
    },
  },

  methods: {
    setCursorCoords({ offsetX, offsetY }) {
      const centerX = this.$el.clientWidth / 2;
      const centerY = this.$el.clientHeight / 2;

      this.rotateX = offsetY - centerY;
      this.rotateY = centerX - offsetX;

      const radius = Math.hypot(this.rotateX, this.rotateY);
      const maxRadius = Math.hypot(this.rotateX, centerY);
      this.angle = (this.maxAngle * radius) / maxRadius;
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
    :style="{ width, height, perspective }"
  >
    <slot name="background"></slot>
    <div
      class="inner"
      :style="{ '--transform': transform, transform: transformed && transform, width, height }"
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
  margin: 0;

  .inner {
    transform-style: preserve-3d;
    transition: transform 1s;
    &:hover {
      transition: none;
    }
  }

  ::v-deep .volumeCardLayer {
    position: absolute;
    top: 0;
    left: 0;
  }
}

</style>