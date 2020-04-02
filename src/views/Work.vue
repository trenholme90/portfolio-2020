<template>
  <div data-page-type="work">
    <div class="page-container">
      <section class="section section--full flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>{{ role }}</h1>
          </div>
          <div class="flex" style="">
            <div class="subtitle text-block margin-right">
              <h1>{{ place }}</h1>
            </div>
            <div class="subtitle text-block">
              <h1 class="date">{{ date }}</h1>
            </div>
          </div>
        </div>
        <div class="content-block">
          <p>
            {{ text }}
          </p>
        </div>
        <div class="content-block content-block--full content-block--center">
          <h1>Skills</h1>
          <ul class="content-block__list">
            <li
              v-for="skill in skills"
              :key="skill.index"
              class="content-block__list-item"
            >
              {{ skill }}
            </li>
          </ul>
        </div>
        <hr class="hide-desktop" />
      </section>
      <section class="section section--full flex--column">
        <Slider :sliderImages="images" />
        <div class="full-width" style="height: 100px;">
          <div class="flex--column flex--full-height flex--content-end">
            <footer>
              <Button
                btnClass="btn btn--secondary"
                btnTxt="Previous"
                :btnLink="`/work/${previousRoute}`"
              />
              <Button
                btnClass="btn btn--primary"
                btnTxt="Next"
                :btnLink="`/work/${nextRoute}`"

              />
            </footer>
          </div>
        </div>
      </section>
    </div>
    <!-- <div class="section--hero__img app-background-image asda-img"></div> -->
  </div>
</template>

<script>
import Slider from "../components/Slider.vue";
import Schema from "../schema";
import Button from "../components/Button.vue";

export default {
  name: "work",
  components: {
    Slider,
    Button,
  },
  data: function() {
    return {
      place: "",
      role: "",
      date: "",
      text: "",
      skills: [],
      images: [],
      nextRoute: "",
      previousRoute: "",
      currentRouteIndex: "",
      nextRouteIndex: "",
      previousRouteIndex: ""
    };
  },
  beforeMount() {
    this.dataHandler();
  },
  mounted() {
    this.setRoutes(this.currentRouteIndex, this.nextRouteIndex, this.previousRouteIndex);
  },
  watch: {
    $route() {
      this.dataHandler();
      this.setRoutes(this.currentRouteIndex, this.nextRouteIndex, this.previousRouteIndex);
    }
  },
  methods: {
    dataHandler: function() {
      for (let item in Schema) {
        if (Object.hasOwnProperty.call(Schema, item)) {
          const pageName = Schema[item].page,
                index = Schema[item].index,
                role = Schema[item].role,
                date = Schema[item].date,
                text = Schema[item].text,
                skills = Schema[item].skills,
                images = Schema[item].images,
                currentRoute = this.$route.params.id;

          if (pageName === currentRoute) {
            this.place = pageName;
            this.role = role;
            this.date = date;
            this.text = text;
            this.skills = skills;
            this.images = images;
            this.currentRouteIndex = index;
            this.nextRouteIndex = index + 1;
            this.previousRouteIndex = index - 1;
          }
        }
      }
    },
    setRoutes: function(current, next, prev) {
      console.log(current, next, prev)
      for (let item in Schema) {
        if (Object.hasOwnProperty.call(Schema, item)) {
          const pageName = Schema[item].page,
                index = Schema[item].index,
                nextBtn = document.querySelector('.btn--primary'),
                prevBtn = document.querySelector('.btn--secondary'),
                maxIndexinSchema = Object.keys(Schema).length - 1;

          //this.applyRoutes(index, target, pageName, btn)
          console.log(pageName, index)
          console.log(index === next, this.nextRoute.length === 0)
          if (index === next && this.nextRoute.length === 0) {
            console.log('index is next')
            if (next <= maxIndexinSchema) {
              console.log('next is less than length')
              this.nextRoute = pageName;
            }
          } else if (current === maxIndexinSchema) {
              console.log('current is equal to length')
              nextBtn.classList.add('is-disabled')
          }

          if(index === prev && this.previousRoute.length === 0) {
            console.log('index is prev')
            if (prev >= 0) {
              console.log('prev is greater than 0')
              this.previousRoute = pageName;
            }
          } else if(prev < 0 && this.previousRoute.length === 0) {
              console.log('prev is less than 0')
              prevBtn.classList.add('is-disabled')
          }
        }
      }
    },
    // applyRoutes: function(index, targetIndex, pageName, btn) {

    // }
  }
};
</script>
