<template>
  <section class="app-main">
    <transition name="fade" mode="out-in">
      <router-view :key="$route.fullPath"></router-view>
    </transition>
  </section>
</template>

<script>

  export default {
    name: 'AppMain',
  }
</script>

<style lang="scss" scoped>
</style>
