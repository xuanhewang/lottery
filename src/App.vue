<template>
  <div id="app">
    <router-view :key="Math.random()"/>
  </div>
</template>

<script>
export default {
  name: 'App',
  mounted() {
  	
  }
}
</script>

<style lang="scss">
  @import "~normalize.css";
  @import "./styles/index.scss";
</style>

