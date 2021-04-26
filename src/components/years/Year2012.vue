<script>
import VolumeCard from "@/components/VolumeCard";
import VolumeCardLayer from "@/components/VolumeCardLayer";

export default {
  name: "Year2012",

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
      { name: "leafs2", elevation: -1 },
      { name: "fruits", elevation: 1 },
      { name: "frame", elevation: 1 },
      { name: "fruitWithEyes", elevation: 2 },
      { name: "leafs1", elevation: 3 },
      { name: "hair", elevation: 4 },
      { name: "girl", elevation: 4 },
      { name: "stars", elevation: 10 },
    ],
  }),
};
</script>

<template>
  <VolumeCard :width="width" :height="height" @toggle="isActive = !isActive">
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
      :src="`/cards/2012/${layer.name}.png`"
      :elevation="layer.elevation"
      :style="[layer.style, isActive && layer.activeStyle]"
      :width="width"
      :height="height"
    />
  </VolumeCard>
</template>

<style lang="scss">
</style>