<template>
  <div id="app">
    <nav-bar />
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
  import NavBar from './components/NavBar';

  export default {
    components: { NavBar },
    name: 'app',
  };
</script>

<style lang="scss">
  @import "~spectre.css";
</style>
