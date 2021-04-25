<script>
export default {
  name: "VolumeCard",

  props: {
    width: {
      type: Number,
      default: 360,
    },
    maxWidth: {
      type: String,
      default: "100%",
    },
    height: {
      type: Number,
      default: 640,
    },
    perspective: {
      type: String,
      default: "1000px",
    },
    maxAngle: {
      type: Number,
      default: 30,
    },
    touchDelay: {
      type: Number,
      default: 100,
    },
  },

  data: () => ({
    rotateX: 0,
    rotateY: 0,
    angle: 0,
    transformed: null,
    touch: null,
    scrollBlocked: true,
  }),

  computed: {
    transform() {
      return `rotate3d(${this.rotateX}, ${this.rotateY}, 0, ${this.angle}deg)`;
    },
    wrapperStyle() {
      const style = {
        perspective: this.perspective,
        "touch-action": this.scrollBlocked ? "none" : null,
      };
      return style;
    },
  },

  methods: {
    mouseMove({ offsetX, offsetY }) {
      // const centerX = this.$el.clientWidth / 2;
      // const centerY = this.$el.clientHeight / 2;

      this.setTransformation(offsetX, offsetY);

      // this.rotateX = offsetY - centerY;
      // this.rotateY = centerX - offsetX;

      // const radius = Math.hypot(this.rotateX, this.rotateY);
      // const maxRadius = Math.hypot(centerX, centerY);
      // const angle = (this.maxAngle * radius) / maxRadius;
      // this.angle = angle > this.maxAngle ? this.maxAngle : angle;
    },

    getTouchCoords(e) {
      if (!this.touch) return;

      if (this.touch.isMoving) {
        e.preventDefault();

        // block scroll
        document.querySelector("html").classList.add("no-scroll");

        const touch = e.touches[0];

        const rect = touch.target.getBoundingClientRect();
        const offsetX = touch.pageX - rect.x;
        const offsetY = touch.pageY - rect.y;

        this.setCursorCoords({ offsetX, offsetY });
      } else if (e.timeStamp - this.touch.timeStamp > this.touchDelay) {
        this.touch.isMoving = true;
        this.transformed = true;
      } else {
        this.touch = null;
      }
    },

    touchMove(e) {
      if (!this.touch) return;

      // FIXME нужно что-то решать со скроллом
      if (true) {
        // if (this.touch.isMoving || e.timeStamp - this.touch.timeStamp > this.touchDelay) {

        this.touch.isMoving = true;

        // block scroll
        // document.querySelector("body").classList.add("no-scroll");

        // FIXME реальная дельта выглядит вяленько, пока пусть будет множитель
        // const offsetX = e.changedTouches[0].clientX * 2;
        // const offsetY = e.changedTouches[0].clientY * 2;
        const offsetX = e.changedTouches[0].clientX;
        const offsetY = e.changedTouches[0].clientY;
        const centerX = this.touch.clientX;
        const centerY = this.touch.clientY;

        this.setTransformation(offsetX, offsetY, centerX, centerY);
      } else {
        this.touch = null;
      }
    },

    touchStart(e) {
      // this.scrollBlocked = true
      this.touch = e.targetTouches[0];
      this.touch.timeStamp = e.timeStamp;
    },

    touchEnd() {
      this.touch = null;
      // this.scrollBlocked = false
      // document.querySelector("body").classList.remove("no-scroll");
      this.cardLeave();
    },

    setTransformation(
      offsetX,
      offsetY,
      centerX = this.width / 2,
      centerY = this.height / 2
    ) {
      const rotateX = offsetY - centerY;
      const rotateY = centerX - offsetX;
      const radius = Math.hypot(rotateX, rotateY);
      const maxRadius = Math.hypot(centerX, rotateX);
      const angle = (this.maxAngle * radius) / maxRadius;

      this.rotateX = rotateX;
      this.rotateY = rotateY;
      this.angle = Math.abs(angle > this.maxAngle) ? this.maxAngle : angle;

      this.transformed = true;
    },

    clearTransformation() {
      this.transformed = null;
      this.angle = 0;
      this.rotateX = 0;
      this.rotateY = 0;
    },

    cardEnter(e) {
      // this.transformed = true;
      this.$emit("toggle");
    },

    cardLeave() {
      this.clearTransformation();
      this.$emit("toggle");
    },
  },
};
</script>

<template>
  <figure
    class="volumeCard"
    @mousemove="mouseMove"
    @mouseenter="cardEnter"
    @mouseleave="cardLeave"
    @touchmove.stop="touchMove"
    @touchstart.stop="touchStart"
    @touchend="touchEnd"
    :style="wrapperStyle"
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
  // touch-action: none;
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