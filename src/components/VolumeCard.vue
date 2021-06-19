<script>
export default {
  name: "VolumeCard",

  props: {
    width: {
      type: String,
      default: "360px",
    },
    maxWidth: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "640px",
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
    angle: 0,
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
      const angle = (this.maxAngle * radius) / maxRadius;
      this.angle = angle > this.maxAngle ? this.maxAngle : angle
    },
    getTouchCoords(e) {
      const touch = e.touches[0]
      const rect = touch.target.getBoundingClientRect();
      const offsetX = touch.pageX - rect.x;
      const offsetY = touch.pageY - rect.y;

      this.setCursorCoords({ offsetX, offsetY });
    },
    mouseEnter() {
      this.transformed = true;
      this.$emit("toggle");
    },
    mouseLeave() {
      this.transformed = null;
      this.$emit("toggle");
    },
  },
};
</script>

<template>
  <figure
    class="volumeCard"
    @mousemove="setCursorCoords"
    @mouseenter="mouseEnter"
    @mouseleave="mouseLeave"
    @touchmove="getTouchCoords"
    @touchstart="mouseEnter"
    @touchend="mouseLeave"
    :style="{ perspective }"
  >
    <slot name="background"></slot>
    <div class="inner" :style="{ transform: transformed && transform }">
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
  touch-action: none;
  margin: 0 auto;
  width: 100%;
  padding-top: 1920px / 1080px * 100%;

  .inner {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    transform-style: preserve-3d;
    transition: transform 1s;
    &:hover {
      transition: transform 0.1s;
    }
  }

  :deep .volumeCardLayer {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
</style>