<template>
  <div id="app">
    <div class="bg-gradient"></div>
    <div class="bg-gradient bg-gradient--bottom"></div>
    <Header />
    <transition name="fadeY">
      <router-view :key="$route.name + ($route.params.id || '')"/>
    </transition>
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
