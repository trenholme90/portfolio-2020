<template>
  <img :class="logoClss" alt="James Trenholme" src="../assets/svgs/logo.svg" />
</template>

<script>
export default {
  name: "Logo",
  props: ["logoClass"],
  data: function() {
    return {
      logoClss: this.logoClass
    };
  }
};
</script>
