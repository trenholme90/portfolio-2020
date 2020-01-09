<template>
  <div class="header">
    <Nav />
    <Logo />
  </div>
</template>

<script>
import Nav from "./Nav.vue";
import Logo from "./Logo.vue";
export default {
  name: "Header",
  components: {
    Nav,
    Logo
  }
};
</script>s