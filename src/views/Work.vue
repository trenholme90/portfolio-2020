<template>
  <div
    data-page-type="work"
    :key="place"
    :class="[{ 'animate-in': animate }, { 'animate-out': !animate }]"
  >
    <!-- <div class="swiper">

    </div> -->
    <div class="page-container">
      <section
        class="section section--full flex--column flex-desktop--content-center"
      >
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>{{ role }}</h1>
          </div>
          <div class="flex margin-top margin-bottom">
            <div class="subtitle text-block text-block--small margin-right">
              <h1>{{ place }}</h1>
            </div>
            <div class="subtitle text-block text-block--small">
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
          <h1 class="margin-bottom">Skills</h1>
          <ul class="content-block__list">
            <li
              v-for="skill in skills"
              :key="skill.index"
              class="content-block__list-item"
            >
              <div :class="['badge', skill.clss]">
                <span>{{ skill.type }}</span>
              </div>
            </li>
          </ul>
        </div>
        <hr class="hide-desktop" />
      </section>
      <section class="section section--full flex--column">
        <Slider :sliderImages="images" :link="link" :key="images.length" />
        <div class="full-width" style="height: 100px;">
          <div class="flex--column flex--full-height">
            <footer>
              <Button
                :btnClass="`btn btn--secondary ${prevIsDisabled}`"
                :isDisabled="prevIsDisabled"
                btnTxt="Previous"
                :btnLink="`/work/${previousRoute}`"
                :key="previousRouteIndex"
              />
              <Button
                :btnClass="`btn btn--primary ${nextIsDisabled}`"
                :isDisabled="nextIsDisabled"
                btnTxt="Next"
                :btnLink="`/work/${nextRoute}`"
                :key="nextRouteIndex"
              />
            </footer>
          </div>
        </div>
      </section>
    </div>
    <!-- <div :class="['section--hero__img app-background-image ', heroImage]"></div> -->
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
    Button
  },
  data: function() {
    return {
      place: "",
      role: "",
      date: "",
      text: "",
      skills: [],
      //heroImage: '',
      images: [],
      link: "",
      nextRoute: "",
      previousRoute: "",
      currentRouteIndex: "",
      nextRouteIndex: "",
      previousRouteIndex: "",
      prevIsDisabled: false,
      nextIsDisabled: false,
      animate: false
    };
  },
  beforeMount() {
    this.dataHandler();
  },
  mounted() {
    this.checkScrollPosition();
    this.setRoutes(
      this.currentRouteIndex,
      this.nextRouteIndex,
      this.previousRouteIndex
    );
    this.animate = true;
  },
  beforeRouteUpdate(to, from, next) {
    console.log(to, from);
    this.animate = false;
    setTimeout(() => {
      next();
    }, 1600);
  },
  beforeRouteLeave(to, from, next) {
    console.log(to, from, next);
    this.animate = false;
    setTimeout(() => {
      next();
    }, 1600);
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
            link = Schema[item].link,
            images = Schema[item].images,
            currentRoute = this.$route.params.id;

          if (pageName === currentRoute) {
            this.place = pageName;
            this.role = role;
            this.date = date;
            this.text = text;
            this.skills = skills;
            this.link = link;
            //this.heroImage = this.formatName(pageName);
            this.images = images;
            this.currentRouteIndex = index;
            this.nextRouteIndex = index + 1;
            this.previousRouteIndex = index - 1;
          }
        }
      }
    },
    setRoutes: function(current, next, prev) {
      this.routeMatch(prev);
      this.routeMatch(prev, next, current);
    },
    routeMatch: function(prev, next, current) {
      for (let item in Schema) {
        if (Object.hasOwnProperty.call(Schema, item)) {
          const vm = this,
            pageName = Schema[item].page,
            index = Schema[item].index;

          if (next) {
            const maxIndexinSchema = Object.keys(Schema).length - 1;
            const nextRoute = this.findNextRoute(
              vm,
              index,
              current,
              next,
              maxIndexinSchema,
              pageName
            );
            if (nextRoute) return (this.nextRoute = nextRoute);
          } else {
            const previousRoute = this.findPreviousRoute(
              vm,
              index,
              prev,
              pageName
            );
            if (previousRoute) return (this.previousRoute = previousRoute);
          }
        }
      }
    },
    findPreviousRoute: function(vm, index, prev, pageName) {
      const target = [];

      this.prevIsDisabled = "";
      if (index === prev && prev >= 0) {
        target.push(pageName);
      } else if (prev < 0) {
        this.prevIsDisabled = "is-disabled";
      }
      return target[0];
    },
    findNextRoute: function(
      vm,
      index,
      current,
      next,
      maxIndexinSchema,
      pageName
    ) {
      const target = [];

      this.nextIsDisabled = "";
      if (index === next && next <= maxIndexinSchema) {
        target.push(pageName);
      } else if (current === maxIndexinSchema) {
        this.nextIsDisabled = "is-disabled";
      }
      return target[0];
    },
    checkScrollPosition: function() {
      const header = document.querySelector(".header"),
        headerPos = header.getBoundingClientRect().top,
        scrollElement = document.querySelector("#app"),
        scrollOptions = {
          top: 0,
          left: 0,
          behavior: "smooth"
        };

      if (headerPos < 0) scrollElement.scrollTo(scrollOptions);
    }
    // formatName: function(pageName) {
    //   const name = pageName.replace(/\s+/g, '-').toLowerCase();
    //   return name
    // }
  }
};
</script>
