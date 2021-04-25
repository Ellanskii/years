<template>
  <section class="yearsContainer">
    <Year2007 />
    <Year2009 />
    <Year2010 />
    <Year2011 />
  </section>
</template>

<script>
import Year2007 from "./components/years/Year2007";
import Year2009 from "./components/years/Year2009";
import Year2010 from "./components/years/Year2010";
import Year2011 from "./components/years/Year2011";

export default {
  components: {
    Year2007,
    Year2009,
    Year2010,
    Year2011,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.yearsContainer {
  display: flex;
  gap: 24px;
}
</style>
