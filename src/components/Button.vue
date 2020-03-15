<template>
  <router-link
    :to="{ link }"
    :data-page="{ link }"
    class="btn__container"
  >
    <button :class="clss">{{ txt }}</button>
  </router-link>
</template>

<script>
export default {
  name: "Button",
  props: ["btnClass", "btnTxt", "btnLink"],
  data: function() {
    return {
      clss: this.btnClass,
      txt: this.btnTxt,
      link: this.btnLink
    };
  }
};
</script>
