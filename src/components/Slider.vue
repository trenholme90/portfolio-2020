<template>
  <div class="slider">
    <transition name="fade">
      <div :v-if="isShowing"  class="slider__inner">
          <img :src="sliderImg" class="slider__img" />
      </div>
    </transition>
    <div class="slider__nav">
      <span v-for="dot in images" :key="dot.index" class="slider__dot" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Slider",
  props: ["sliderImages"],
  data: function() {
    return {
      images: this.sliderImages,
      sliderImg: this.sliderImages[0],
      isShowing: true
    };
  },
  mounted() {
    const dots = document.querySelectorAll(".slider__dot");
    dots[0].classList.add('is-active');

    for(let [dot, index] of dots.entries()) {
      this.sliderBinding(dot, index, this.images, dots)
    }
  },
  methods: {
    sliderBinding: function(index, dot, images, arrayDots) {
      const targetSrc = this.returnTargetSrc(index, images)
      const vm = this
      dot.addEventListener('click', function() {
        vm.removeAllInstancesOfClass(arrayDots, "is-active")
        vm.changeImgSrc(targetSrc, vm)
        this.classList.add("is-active")
      })   
    },
    returnTargetSrc: (index, images) => {
      const imgList = images;
      let targetSrc = [];
      for(let [imgIndex, imgSrc] of imgList.entries()) {
        if(imgIndex === index) {
          targetSrc.push(imgSrc)
        }
      }
      return targetSrc[0]
    },
    changeImgSrc: (targetSrc, vm) => {
      const sliderImg = document.querySelector(".slider__img");
      console.log(vm)
      vm.$data.isShowing = false
      sliderImg.src = targetSrc;
      
    },
    removeAllInstancesOfClass: (elements, clss) => {
      for(let el of elements) {
        if(el.classList.contains(clss)) el.classList.remove(clss)
      }
    }
  }
};
</script>
