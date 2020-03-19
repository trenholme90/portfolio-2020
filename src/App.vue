<template>
  <div id="app">
    <div class="bg-gradient"></div>
    <div class="bg-gradient bg-gradient--bottom"></div>
    <Header />
    <router-view />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";

export default {
  name: "app",
  components: {
    Header
  }
};
</script>

<style lang="scss">
@import "/assets/styles/main";
</style>
