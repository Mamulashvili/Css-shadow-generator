<template>
  <box-shadow />
</template>

<script>
import BoxShadow from "./components/BoxShadow.vue";

export default {
  name: "App",
  components: {
    BoxShadow,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.flex {
  display: flex;
}

.flex-center {
  justify-content: center;
  align-items: center;
}

.flex-spc-btwn {
  justify-content: space-between;
}
</style>
