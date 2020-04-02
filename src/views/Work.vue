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
                :btnLink="previousRoute"
              />
              <Button
                btnClass="btn btn--primary"
                btnTxt="Next"
                :btnLink="nextRoute"

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
      previousRoute: ""
    };
  },
  beforeMount() {
    this.dataHandler();
  },
  watch: {
    $route() {
      this.dataHandler();
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

          let currentRouteIndex,
              nextRouteIndex,
              previousRouteIndex;

          if (pageName === currentRoute) {

            this.place = pageName;
            this.role = role;
            this.date = date;
            this.text = text;
            this.skills = skills;
            this.images = images;

            currentRouteIndex = index;
            nextRouteIndex = index + 1;
            previousRouteIndex = index - 1;

            this.setRoutes(currentRouteIndex, nextRouteIndex, previousRouteIndex);
          }
        }
      }
    },
    setRoutes: function(current, next, prev) {
      console.log(current, next, prev)

    }
  }
};
</script>
