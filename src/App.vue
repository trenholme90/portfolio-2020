<template>
  <div id="app">
    <Header />
    <transition name="fadeY">
      <router-view :key="$route.name + ($route.params.id || '')" v-on:background="setBackground"/>
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
