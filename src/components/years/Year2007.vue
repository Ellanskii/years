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
      { name: "frame", elevation: 1 },
      { name: "girl", elevation: 4 },
      { name: "blazer", elevation: 8 },
      { name: "stars", elevation: 15 },
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