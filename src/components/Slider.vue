<template>
  <div class="slider">
    <transition name="fade">
      <div :v-if="isShowing" class="slider__inner">
        <!-- <img :src="sliderImg" class="slider__img" /> -->
        <div
          v-bind:style="{ 'background-image': `url('${sliderImg}')` }"
          class="slider__img"
        ></div>
      </div>
    </transition>
    <div class="slider__nav">
      <div class="slider__counter">
        {{ `0${activeIndex}/0${imgQuant}` }}
      </div>
      <div class="slider__dot-container hide-mobile">
        <span v-for="dot in images" :key="dot.index" class="slider__dot" />
      </div>
      <div>
          <Chevron clss="chevron chevron--left" />
          <Chevron clss="chevron chevron--right" />
      </div>
    </div>
  </div>
</template>

<script>
import Chevron from "./icons/Chevron.vue";
export default {
  name: "Slider",
  props: ["sliderImages"],
  components: {
    Chevron
  },
  data: function() {
    return {
      images: this.sliderImages,
      sliderImg: this.sliderImages[0],
      isShowing: true,
      activeIndex: "1",
      imgQuant: ""
    };
  },
  mounted() {
    const dots = document.querySelectorAll(".slider__dot"),
          previousArrow = document.querySelector('.chevron--left'),
          nextArrow = document.querySelector('.chevron--right'),
          arrows = [previousArrow, nextArrow],
          vm = this;
    this.imgQuant = dots.length
    dots[0].classList.add("is-active");

    for (let [dot, index] of dots.entries()) {
      this.sliderBinding(dot, index, this.images, dots, vm);
    }

    for (let [index, arrow] of arrows.entries()) {
      this.arrowBinding(arrow, previousArrow, nextArrow, index, this.images, dots, vm);
    }
  },
  methods: {
    sliderBinding: function(index, dot, images, arrayDots, vm) {
      const targetInfo = this.returnTargetFromArray(index, images),
            targetSrc = targetInfo[0],
            targetIndex = parseInt(targetInfo[1])

      dot.addEventListener("click", function() {
        vm.removeAllInstancesOfClass(arrayDots, "is-active");
        vm.changeImgSrc(targetSrc, targetIndex, vm);
        this.classList.add("is-active");
      });
    },
    arrowBinding: (arrow, previousArrow, nextArrow, index, images, dots, vm) => {
      arrow.addEventListener("click", function() {
        const currentIndexForDisplay = parseInt(vm.activeIndex),
              currentIndex = currentIndexForDisplay - 1,
              previousIndex = currentIndex - 1,
              nextIndex = currentIndex + 1
        vm.removeAllInstancesOfClass(dots, "is-active");

        if(arrow === nextArrow) {
          const nextTargetInfo = vm.returnTargetFromArray(nextIndex, images),
                nextTargetSrc = nextTargetInfo[0],
                nextTargetIndex = nextTargetInfo[1],
                isNext = true;

          vm.changeImgSrc(nextTargetSrc, nextTargetIndex, vm, isNext)
          const targetDot = vm.returnTargetFromArray(nextIndex, dots);
          targetDot[0].classList.add("is-active");
        } else if (arrow === previousArrow) { 
          const previousTargetInfo = vm.returnTargetFromArray(previousIndex, images),
                previousTargetSrc = previousTargetInfo[0],
                previousTargetIndex = previousTargetInfo[1],
                isPrevious = true;

          vm.changeImgSrc(previousTargetSrc, previousTargetIndex, vm, isPrevious)
          const targetDot = vm.returnTargetFromArray(previousTargetIndex, dots);
          targetDot[0].classList.add("is-active");
        }
      })
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
    changeImgSrc: (targetSrc, targetIndex, vm, isNextOrPrevious) => {
      const sliderImg = document.querySelector(".slider__img"),
            sliderImgSrc = sliderImg.style.backgroundImage
            
      if(isNextOrPrevious) {
        if(targetIndex + 1 > vm.$data.imgQuant ||
        targetIndex - 1 < vm.$data.imgQuant) {
          sliderImg.style.backgroundImage = sliderImgSrc;
        } else {
          vm.$data.activeIndex = targetIndex + 1;
          vm.$data.isShowing = false;
          sliderImg.style.backgroundImage = `url('${targetSrc}')`;
        }
      }
      vm.$data.activeIndex = targetIndex + 1;
      vm.$data.isShowing = false;
      sliderImg.style.backgroundImage = `url('${targetSrc}')`;
    },
    removeAllInstancesOfClass: (elements, clss) => {
      for (let el of elements) {
        if (el.classList.contains(clss)) el.classList.remove(clss);
      }
    }
  }
};
</script>
