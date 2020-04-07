<template>
  <div class="header">
    <transition name="fadeY" style="transition-delay: .25s">
      <Nav v-show="animate" />
    </transition>
  </div>
</template>

<script>
import Nav from "./Nav.vue";
export default {
  name: "Header",
  components: {
    Nav
  },
  data: () => {
    return {
      animate: false
    };
  },
  mounted() {
    this.animate = true
  }
};
</script>
