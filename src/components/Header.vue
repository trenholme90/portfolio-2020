<template>
  <div :class="[ 'header', { 'animate-in': animate }, { 'animate-out': !animate }]">
    <Nav />
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
    setTimeout(() => {
      this.animate = true;
    }, 100);
  }
};
</script>
