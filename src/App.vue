<template>
  <div id="app">
    <Header />
    <transition mode="out-in">
      <router-view :key="$route.name + ($route.params.id || '')" />
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
