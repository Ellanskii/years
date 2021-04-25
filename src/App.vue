<script>
import Year2007 from "./components/years/Year2007";
import Year2009 from "./components/years/Year2009";
import Year2010 from "./components/years/Year2010";
import Year2011 from "./components/years/Year2011";

import { debounce } from "lodash";

export default {
  components: {
    Year2007,
    Year2009,
    Year2010,
    Year2011,
  },

  data: () => ({
    cardWidth: 320,
  }),

  computed: {
    cardHeight() {
      return this.cardWidth * 1.77777777778; // 16/9
    }
  },

  methods: {
    setCardWidth() {
      this.cardWidth = document.querySelector(".volumeCard").clientWidth;
    },
  },

  mounted() {
    this.setCardWidth();
    window.addEventListener("resize", debounce(this.setCardWidth, 100));
  },
};
</script>

<template>
  <section class="yearsContainer">
    <Year2007 :width="cardWidth" :height="cardHeight" />
    <Year2009 :width="cardWidth" :height="cardHeight" />
    <Year2010 :width="cardWidth" :height="cardHeight" />
    <Year2011 :width="cardWidth" :height="cardHeight" />
  </section>
</template>


<style lang="scss">
:root {
  --gap: 24px;
  @media screen and (min-width: 720px) {
    --gap: 56px;
  }
}
html {
  background: #232127;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: calc(var(--gap) * 1.5);
}

.yearsContainer {
  display: grid;
  gap: var(--gap);
  // max-width: 1360px;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  margin: 0 auto;
}
</style>
