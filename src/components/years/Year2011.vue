<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2011",

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
      {
        name: "fire",
        elevation: -10,
        style: { transition: "transform 5s" },
        activeStyle: { transform: "translateZ(-200px)" },
      },
      { name: "cat", elevation: -5 },
      { name: "frame", elevation: 1 },
      {
        name: "mask",
        elevation: 6,
        style: { transition: "transform 5s" },
        activeStyle: { transform: "translateZ(100px)" },
      },
      {
        name: "mashroom1",
        elevation: 2,
        // style: { transition: "transform 1s" },
        // activeStyle: { transform: "translate3d(5%, -8%, 30px)", transition: "transform .20s ease-out" },
      },
      {
        name: "mashroom2",
        elevation: 6,
        // style: { transition: "transform 1s" },
        // activeStyle: { transform: "translate3d(-7%, 9%, 70px)", transition: "transform .22s ease-out" },
      },
      {
        name: "mashroom3",
        elevation: 9,
        // style: { transition: "transform 1s" },
        // activeStyle: { transform: "translate3d(8%, 8%, 100px)", transition: "transform .21s ease-out" },
      },
      {
        name: "stars",
        elevation: 5,
        // style: { transition: "transform 1s" },
        // activeStyle: { transform: "translateZ(200px)" },
      },
    ],
  }),
};
</script>

<template>
  <VolumeCard :width="width" :height="height" @toggle="isActive = !isActive">
    <template #background>
      <VolumeCardLayer
        src="/cards/2011/background.png"
        :width="width"
        :height="height"
      />
    </template>
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2011/${layer.name}.png`"
      :elevation="layer.elevation"
      :style="[layer.style, isActive && layer.activeStyle]"
      :width="width"
      :height="height"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>