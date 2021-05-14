<script>
import Year2007 from "./components/years/Year2007";
import Year2009 from "./components/years/Year2009";
import Year2010 from "./components/years/Year2010";
import Year2011 from "./components/years/Year2011";
import Year2012 from "./components/years/Year2012";
import Year2014 from "./components/years/Year2014";

import { debounce } from "lodash";

export default {
  components: {
    Year2007,
    Year2009,
    Year2010,
    Year2011,
    Year2012,
    Year2014
  },

  data: () => ({
    cardWidth: 320,
  }),

  computed: {
    cardHeight() {
      return this.cardWidth * 1.77777777778; // 16/9
    },
  },

  mounted() {
    this.setCardWidth();
    window.addEventListener("resize", debounce(this.setCardWidth, 100));
  },

  methods: {
    setCardWidth() {
      this.cardWidth = document.querySelector(".volumeCard").clientWidth;
    },
  },
};
</script>

<template>
  <section class="yearsContainer">
    <Year2007
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#ac022d' }"
    />
    <Year2009
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#f8bd41' }"
    />
    <Year2010
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#00baab' }"
    />
    <Year2011
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#ee406e' }"
    />
    <Year2012
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#e04f3c' }"
    />
    <Year2014
      :width="cardWidth"
      :height="cardHeight"
      :style="{ background: '#b563a3' }"
    />
  </section>
</template>


<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
:root {
  --page-padding: 56px;
  --gap: 56px;
  --min-card-width: 200px;

  @media screen and (min-width: 420px) {
    --gap: 48px;
    --page-padding: 56px;
    --min-card-width: 300px;
  }
  @media screen and (min-width: 1024px) {
    --gap: 56px;
    --page-padding: 72px;
    --min-card-width: 320px;
  }
}

html {
  background: #232127;
  padding: var(--page-padding);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.yearsContainer {
  display: grid;
  gap: var(--gap);
  // max-width: 1360px;
  grid-template-columns: repeat(auto-fill, minmax(var(--min-card-width), 1fr));
  margin: 0 auto;
}

.no-scroll {
  height: 100%;
  overflow: hidden;
  width: 100%;
  position: fixed;
}
</style>
