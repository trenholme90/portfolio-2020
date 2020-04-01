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
        <Slider :sliderImages="images" :key="images.length" />
        <div class="full-width" style="height: 100px;">
          <div class="flex--column flex--full-height">
            <footer>
              <Button
                btnClass="btn btn--secondary"
                btnTxt="Previous"
                :btnLink="pageFrom.path"
              />
              <Button
                btnClass="btn btn--primary"
                btnTxt="Next"
                :btnLink="pageTo.path"

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
      pageTo: "",
      pageFrom: ""
    };
  },
  beforeMount() {
    this.dataHandler();
  },
  beforeUpdate () {
    this.dataHandler();
  },
  watch: {
    $route(to, from) {
      this.pageTo = to
      this.pageFrom = from
      console.log(this.pageTo, this.pageFrom)
    }
  },
  methods: {
    dataHandler: function() {
      for (let item in Schema) {
        if (Object.hasOwnProperty.call(Schema, item)) {
          const pageName = Schema[item].page,
                currentRoute = this.$route.params.id;

          if (pageName === currentRoute) {
            const role = Schema[item].role,
                  date = Schema[item].date,
                  text = Schema[item].text,
                  skills = Schema[item].skills,
                  images = Schema[item].images;

            this.place = pageName;
            this.role = role;
            this.date = date;
            this.text = text;
            this.skills = skills;
            this.images = images;
          }
        }
      }
    }
  }
};
</script>
