<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2014",

  components: {
    VolumeCard,
    VolumeCardLayer,
  },

  props: {
    width: {
      type: Number,
      default: 360,
    },
    height: {
      type: Number,
      default: 640,
    },
  },

  data: () => ({
    isActive: false,
    layers: [
      // { name: "cube", elevation: 5 },
      // { name: "frame", elevation: 4 },
      // { name: "cloud_1", elevation: 2, style: { transform: 'translateZ(50px) rotateY(45deg)' }, },
      // { name: "cloud_2", elevation: 3 },
      // { name: "cloud_3", elevation: 4 },
      // { name: "cloud_4", elevation: 4 },
      // { name: "sun", elevation: 2 },
      // { name: "girl", elevation: 5 },
      { name: "cube", elevation: 0 },
      // { name: "test", elevation: 0, style: { transform: 'translateZ(50px) rotateY(45deg)' }, },
    ],
  }),
};
</script>

<template>
  <VolumeCard
    :width="width"
    :height="height"
    @toggle="isActive = !isActive"
  >
    <!-- <template #background>
      <VolumeCardLayer
        src="/cards/2011/background.png"
        :width="width"
        :height="height"
      />
    </template> -->
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2014/${layer.name}.png`"
      :elevation="layer.elevation"
      :style="layer.style"
      :width="width"
      :height="height"
      perspective="0"
    />
    <VolumeCardLayer
      src="/cards/2014/test.png"
      width="61"
      height="27"
      perspective="0"
    />
    <img :src="require(`@/assets/cards/2014/test.png`)" alt="" class="test"/>
    <img :src="require(`@/assets/cards/2014/cube.svg`)" alt="" class="test cube" style="transform: rotateX(90deg) rotateY(45deg)" />
  </VolumeCard>
</template>

<style lang="scss">
.test {
  object-fit: contain;
  width: 100%;
  height: 100%;
  object-position: center;
  position: absolute;
  top: 0;
  left: 0;
}
.cube {
  width: 50%;
  height: auto;
}
</style>