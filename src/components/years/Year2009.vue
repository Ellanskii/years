<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2009",

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
      { name: "frame", elevation: 1 },
      { name: "leftHand", elevation: 4 },
      { name: "cocktail", elevation: 2 },
      { name: "rightHand", elevation: 5 },
      { name: "leafOne", elevation: 4 },
      { name: "stem2", elevation: 6 },
      { name: "leafs", elevation: 6 },
      { name: "flowers", elevation: 6 },
      { name: "flower", elevation: 8 },
      { name: "stars", elevation: 15 },
    ],
  }),
};
</script>

<template>
  <VolumeCard :width="width" :height="height">
    <template #background>
      <VolumeCardLayer
        :width="width"
        :height="height"
        src="/cards/2009/background.png"
      />
    </template>
    <VolumeCardLayer
      v-for="(layer, index) in layers"
      :key="index"
      :src="`/cards/2009/${layer.name}.png`"
      :elevation="layer.elevation"
      :width="width"
      :height="height"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>