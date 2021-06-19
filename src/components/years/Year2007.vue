<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2007",

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
    layers: [
      { name: "girl", elevation: -8 },
      { name: "blazer", elevation: -4 },
      { name: "frame", elevation: 1 },
      { name: "stars", elevation: 10 },
    ],
  }),
};
</script>

<template>
  <VolumeCard>
    <template #background>
      <VolumeCardLayer
        :width="width"
        :height="height"
        src="/cards/2007/background.png"
      />
    </template>
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2007/${layer.name}.png`"
      :elevation="layer.elevation"
      :width="width"
      :height="height"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>