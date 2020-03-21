<template>
  <div data-page-type="work">
    <div class="page-container">
      <section class="section section--full flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>Web Designer</h1>
          </div>
          <div class="flex" style="">
            <div class="subtitle text-block margin-right">
              <h1>ASDA</h1>
            </div>
            <div class="subtitle text-block">
              <h1 class="date">Mar 2016 - Oct 2017</h1>
            </div>
          </div>
        </div>
        <div class="content-block">
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quasi doloribus quam aliquam minus nihil ad enim provident fugit dignissimos id tenetur reiciendis natus assumenda veritatis, officia dolor rerum aut eaque.
          </p>
        </div>
        <div class="content-block content-block--full content-block--center">
          <h1>Skills</h1>
          <ul class="content-block__list">
            <li class="content-block__list-item"><p>HTML</p></li>
            <li class="content-block__list-item"><p>CSS</p></li>
            <li class="content-block__list-item"><p>Javascript</p></li>
            <li class="content-block__list-item"><p>PhotoShop</p></li>
            <li class="content-block__list-item"><p>Illustrator</p></li>
          </ul>
        </div>
        <!-- <div class="content-block">
          <span class="chevron chevron--down flex--content-center"></span>
        </div> -->
        <hr class="hide-desktop" />
      </section>
      <section class="section section--full flex--column">
        <!-- <div class="content-block content-block--full content-block--center">
          <ul class="content-block__list">
            <li class="content-block__list-item content-block__list-img fade-animation"><img src="https://trenholme90.github.io/images/Toni&Guy-screenshot.jpg" /></li>
            <li class="content-block__list-item content-block__list-img"><img src="https://trenholme90.github.io/images/Bacardi-screenshot.jpg" /></li>
          </ul>
        </div> -->
        <Slider
          :sliderImages="[
            'https://trenholme90.github.io/images/Toni&Guy-screenshot.jpg',
            'https://trenholme90.github.io/images/Bacardi-screenshot.jpg'
          ]"
        />
      </section>
    </div>
    <div class="section--hero__img app-background-image asda-img"></div>
  </div>
</template>

<script>
import Slider from "../components/Slider.vue";
export default {
  name: "work",
  components: {
    Slider
  }
};
</script>
