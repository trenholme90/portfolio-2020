<template>
  <div id="app" :class="{ 'is-landscape': isLandscape }">
    <div class="bg-gradient"></div>
    <div class="bg-gradient bg-gradient--bottom"></div>
    <div class="fog"></div>
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
  },
  data: () => {
    return {
      isLandscape: false
    };
  },
  beforeMount() {
    if (window.DeviceOrientationEvent) {
      this.orientation();
      window.addEventListener("orientationchange", this.orientation);
    }
  },
  methods: {
    orientation: function() {
      window.innerHeight < window.innerWidth
        ? (this.isLandscape = false)
        : (this.isLandscape = true);
    }
  }
};
</script>

<style lang="scss">
@import "/assets/styles/main";
</style>
