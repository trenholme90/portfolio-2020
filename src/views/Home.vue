<template>
  <div
    data-page-type="home"
    :class="[{ 'animate-in': animate }, { 'animate-out': !animate }]"
  >
    <!-- <div class="swiper">
      <Logo logo-class="swiper-logo" />
    </div> -->
    <div class="page-container">
      <section class="section section--info flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>James Trenholme</h1>
          </div>
          <div class="margin-top margin-bottom">
            <div class="subtitle text-block text-block--small">
              <h1>Front-end Developer</h1>
            </div>
          </div>
          <p>
            A front-end developer from Leeds, that helps build exciting content
            and user stories.
          </p>
        </div>
        <div class="flex--full-height full-width">
          <div
            class="flex--column flex--content-end flex-desktop--content-center"
          >
            <footer>
              <Button
                btnClass="btn btn--primary"
                btnTxt="Experience"
                btnLink="/work/Jet2"
              />
              <Button
                btnClass="btn btn--secondary"
                btnTxt="Contact"
                btnLink="/contact"
              />
            </footer>
          </div>
        </div>
        <div class="logo-icon__container">
          <Github clss="logo-icon" />
          <Twitter clss="logo-icon" />
          <Email clss="logo-icon" />
        </div>
      </section>
      <div class="section--hero__img"></div>
    </div>
  </div>
</template>

<script>
//import Logo from "../components/Logo.vue";
import Button from "../components/Button.vue";
import Github from "../components/icons/Github.vue";
import Twitter from "../components/icons/Twitter.vue";
import Email from "../components/icons/Email.vue";
export default {
  name: "home",
  components: {
    Button,
    Github,
    Twitter,
    Email
    // Logo
  },
  data: function() {
    return {
      animate: false
    };
  },
  mounted() {
    setTimeout(() => {
      this.animate = true;
    }, 100);
  },
  beforeRouteLeave(to, from, next) {
    console.log(to, from, next);
    this.animate = false;
    setTimeout(() => {
      next();
    }, 1600);
  }
};
</script>
