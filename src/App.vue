<template>
  <div class="Container">
    <IndexPage />
  </div>
</template>

<script>
import IndexPage from "./components/Index.vue";

export default {
  name: "App",
  components: {
    IndexPage,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  list-style-type: none;
  text-decoration: none;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 1200px;
  margin: 0 auto;
}

.Container {
  padding: 20px 0;
}
</style>
