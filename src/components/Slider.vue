<template>
  <div
    class="slider"
    :class="[{ 'animate-in': animate }, { 'animate-out': !animate }]"
  >
    <div :v-if="isShowing" class="slider__inner">
      <a :href="hyperlink">
        <div
          v-bind:style="{ 'background-image': `url('${sliderImg}')` }"
          class="slider__img"
        ></div>
      </a>
    </div>
    <div class="slider__nav">
      <div class="slider__counter">
        {{ `0${activeIndex}/0${imgQuant}` }}
      </div>
      <div class="slider__dot-container hide-mobile">
        <span v-for="dot in images" :key="dot.index" class="slider__dot" />
      </div>
      <div>
        <Chevron clss="chevron chevron--left is-disabled" />
        <Chevron clss="chevron chevron--right" />
      </div>
    </div>
  </div>
</template>

<script>
import Chevron from "./icons/Chevron.vue";
import { setTimeout } from "timers";
export default {
  name: "Slider",
  props: ["sliderImages", "link"],
  components: {
    Chevron
  },
  data: function() {
    return {
      images: this.sliderImages,
      sliderImg: this.sliderImages[0],
      hyperlink: this.link,
      isShowing: true,
      activeIndex: "1",
      imgQuant: "",
      animate: false
    };
  },
  mounted() {
    const dots = this.$el.querySelectorAll(".slider__dot"),
      previousArrow = this.$el.querySelector(".chevron--left"),
      nextArrow = this.$el.querySelector(".chevron--right"),
      arrows = [previousArrow, nextArrow],
      vm = this;

    this.imgQuant = dots.length;
    dots[0].classList.add("is-active");

    for (let [dot, index] of dots.entries()) {
      this.sliderBinding(dot, index, this.images, dots, vm);
    }

    for (let [index, arrow] of arrows.entries()) {
      this.arrowBinding(
        arrow,
        previousArrow,
        nextArrow,
        index,
        this.images,
        dots,
        vm
      );
    }

    this.animate = true;
  },
  beforeRouteUpdate(to, from, next) {
    this.animate = false;
    setTimeout(() => {
      next();
    }, 1600);
  },
  beforeRouteLeave(to, from, next) {
    this.animate = false;
    setTimeout(() => {
      next();
    }, 1600);
  },
  methods: {
    sliderBinding: function(index, dot, images, dots, vm) {
      const targetInfo = vm.returnTargetFromArray(index, images),
        targetSrc = targetInfo[0],
        targetIndex = parseInt(targetInfo[1]);

      dot.addEventListener("click", function() {
        vm.animate = false;
        vm.removeAllInstancesOfClass(dots, "is-active");
        vm.changeImgSrc(targetSrc, targetIndex, vm, dots);
        setTimeout(() => {
          vm.animate = true;
        }, 400);
        setTimeout(() => {
          this.classList.add("is-active");
        }, 800);
      });
    },

    arrowBinding: (
      arrow,
      previousArrow,
      nextArrow,
      index,
      images,
      dots,
      vm
    ) => {
      arrow.addEventListener("click", function() {
        const currentIndexForDisplay = parseInt(vm.activeIndex),
          currentIndex = currentIndexForDisplay - 1,
          previousIndex = currentIndex - 1,
          nextIndex = currentIndex + 1;

        vm.animate = false;
        if (arrow === nextArrow) vm.arrowHandler(nextIndex, images, dots, vm);
        else if (arrow === previousArrow)
          vm.arrowHandler(previousIndex, images, dots, vm);
        setTimeout(() => {
          vm.animate = true;
        }, 400);
      });
    },

    changeImgSrc: (targetSrc, targetIndex, vm, dots, isNextOrPrevious) => {
      const sliderImg = vm.$el.querySelector(".slider__img"),
        previousArrow = vm.$el.querySelector(".chevron--left"),
        nextArrow = vm.$el.querySelector(".chevron--right"),
        arrows = [previousArrow, nextArrow],
        imgQuantIndex = parseInt(vm.imgQuant) - 1;

      if (isNextOrPrevious) {
        // if the target Index is outside of image range
        if (targetIndex === -1 || targetIndex > imgQuantIndex) return;
      }
      vm.removeAllInstancesOfClass(arrows, "is-disabled");

      // if first in the list
      if (targetIndex === 0) {
        previousArrow.classList.add("is-disabled");
        vm.imageHandler(targetIndex, dots, sliderImg, targetSrc, vm);
      }
      // if last in the list
      else if (targetIndex === imgQuantIndex) {
        nextArrow.classList.add("is-disabled");
        vm.imageHandler(targetIndex, dots, sliderImg, targetSrc, vm);
      } else {
        vm.imageHandler(targetIndex, dots, sliderImg, targetSrc, vm);
      }
    },

    imageHandler: (targetIndex, dots, sliderImg, targetSrc, vm) => {
      vm.$data.activeIndex = targetIndex + 1;
      vm.$data.isShowing = false;
      vm.removeAllInstancesOfClass(dots, "is-active");
      setTimeout(() => {
        sliderImg.style.backgroundImage = `url('${targetSrc}')`;
      }, 400);
    },

    arrowHandler: (index, images, dots, vm) => {
      const targetInfo = vm.returnTargetFromArray(index, images),
        targetSrc = targetInfo[0],
        isNextOrPrevious = true;

      let targetIndex = targetInfo[1];
      if (targetIndex == undefined) targetIndex = index;

      vm.changeImgSrc(targetSrc, targetIndex, vm, dots, isNextOrPrevious);
      const targetDot = vm.returnTargetFromArray(index, dots);
      setTimeout(() => {
        if (targetDot[0]) targetDot[0].classList.add("is-active");
      }, 800);
    },

    returnTargetFromArray: (index, array) => {
      let targetSrc = [];
      for (let [itemIndex, item] of array.entries()) {
        if (itemIndex === index) {
          targetSrc.push(item, itemIndex);
        }
      }
      return targetSrc;
    },

    removeAllInstancesOfClass: (elements, clss) => {
      for (let el of elements) {
        if (el.classList.contains(clss)) el.classList.remove(clss);
      }
    }
  }
};
</script>
