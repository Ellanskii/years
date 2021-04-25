<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2007",

  components: {
    VolumeCard,
    VolumeCardLayer,
  },

  data: () => ({
    layers: [
      { name: "stars", elevation: -10 },
      { name: "frame", elevation: 1 },
      { name: "girl", elevation: -8 },
      { name: "blazer", elevation: -4 },
    ],
  }),
};
</script>

<template>
  <VolumeCard>
    <template #background>
      <VolumeCardLayer src="/cards/2007/background.png" />
    </template>
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2007/${layer.name}.png`"
      :elevation="layer.elevation"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>