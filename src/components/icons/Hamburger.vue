<template>
  <div class="hamburger" :class="{ 'is-open': isOpen }">
    <span></span>
    <span></span>
    <span></span>
  </div>
</template>

<script>
export default {
  name: "hamburger",
  props: ["menuIsOpen"],
  data: function() {
    return {
      isOpen: this.menuIsOpen
    };
  }
};
</script>

<style lang="scss" scoped>
@import "../../assets/styles/helper/transition";
.hamburger {
  display: block;
  position: relative;
  z-index: 20;
  user-select: none;
  align-self: center;

  & span {
    display: block;
    width: 33px;
    height: 4px;
    margin-bottom: 5px;
    position: relative;
    background: #cdcdcd;
    border-radius: 3px;
    z-index: 1;
    transform-origin: 4px;
    @extend .default-trans;

    @media screen and (min-width: 768px) {
      width: 43px;
      height: 5px;
      margin-bottom: 8px;
      transform-origin: 3px;
    }
  }
}

.menu.is-open ~ .hamburger span {
  opacity: 1;
  transform: rotate(45deg);
  background: 0.232323;

  &:nth-last-child(2) {
    opacity: 0;
    //transform: rotate(-45deg) translate(8px, 10px);
  }

  &:last-child {
    transform: rotate(-45deg);
  }
}
</style>
