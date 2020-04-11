<template>
  <div id="app">
    <div class="bg-gradient"></div>
    <div class="bg-gradient bg-gradient--bottom"></div>
    <transition name="backgroundReveal">
      <div :class="['section--hero__img app-background-image ', {'hidden': !isbackgroundImg}, backgroundImg ]" v-show="animate"></div>
    </transition>
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
  },
  data: function() {
    return {
      backgroundImg: '',
      isbackgroundImg: false,
      animate: false
    };
  },
  mounted() {
    this.checkClassChange
    this.animate = true
  },
  watch: {
    backgroundImg: function () {
      this.animate = false
      this.checkClassChange()
    }
    // $route() {
    //   this.checkScrollPosition();
    //   this.dataHandler();
    //   this.setRoutes(this.currentRouteIndex, this.nextRouteIndex, this.previousRouteIndex);
    // }
  },
  methods: {
    setBackground (heroImg) {
      this.backgroundImg = heroImg
      this.backgroundImg === "" ? this.isbackgroundImg = false : this.isbackgroundImg = true
    },
    checkClassChange () {
      // Select the node that will be observed for mutations
      const targetNode = document.querySelector('.section--hero__img');
      const vm = this
      // Options for the observer (which mutations to observe)
      const config = { attributes: true};

      // Callback function to execute when mutations are observed
      const callback = function() {
        console.log(vm)
        vm.animate = true
        observer.disconnect()
      };

      // Create an observer instance linked to the callback function
      const observer = new MutationObserver(callback);

      // Start observing the target node for configured mutations
      observer.observe(targetNode, config);

    }
  }
};
</script>

<style lang="scss">
@import "/assets/styles/main";
</style>
