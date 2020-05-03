<template>
  <div class="btn__container" v-on:click="eventHandler">
    <button :class="btnClass">{{ btnTxt }}</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: ["btnClass", "btnTxt", "btnLink", "isDisabled"],
  methods: {
    eventHandler: function() {
      const vm = this,
        $this = this.$el,
        btn = $this.querySelector(".btn");

      if (!btn.classList.contains("is-disabled")) {
        vm.$router.push({ path: vm.btnLink });
        $this.removeEventListener("click", $this);
      }
    }
  }
};
</script>
