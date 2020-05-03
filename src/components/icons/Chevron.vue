<template>
  <span :class="iconClass">
    <svg width="24" height="24">
      <path d="M5 3l3.057-3L20 12 8.057 24 5 21l9-9z" />
    </svg>
  </span>
</template>

<script>
export default {
  name: "chevron",
  props: ["clss"],
  data: function() {
    return {
      iconClass: this.clss
    };
  }
};
</script>

<style lang="scss" scoped>
@import "../../assets/styles/helper/transition";
</style>
