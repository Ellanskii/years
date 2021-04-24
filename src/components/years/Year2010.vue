<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2009",

  components: {
    VolumeCard,
    VolumeCardLayer,
  },

  data: () => ({
    layers: [
      // { name: "clouds", elevation: 1 },
      { name: "frame", elevation: 4 },
      { name: "road", elevation: 3 },
      { name: "dashed", elevation: 4 },
      { name: "leftLeg", elevation: 5 },
      { name: "body", elevation: 6 },
      { name: "bottle", elevation: 10 },
      { name: "skate", elevation: 4 },
      { name: "rightLeg", elevation: 4 },
    ],
  }),
};
</script>

<template>
  <VolumeCard>
    <template #background>
      <VolumeCardLayer src="/cards/2010/background.png" />
      <VolumeCardLayer src="/cards/2010/clouds.png" />
    </template>
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2010/${layer.name}.png`"
      :elevation="layer.elevation"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>