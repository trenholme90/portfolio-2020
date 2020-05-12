<template>
  <div 
    data-page-type="Contact"
    :class="[{ 'animate-in': animate }, { 'animate-out': !animate }]"
  >
    <div class="page-container">
      <section class="section section--info flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>Contact me</h1>
          </div>
          <div class="margin-top--double">
            <p>
              If you like what you see and want to get in contact, please at
              <a class="link" href="mailto:jje.trenholme@gmail.com"
                >jje.trenholme@gmail.com</a
              >
              or reach out for me on one of the platforms below. I look forward
              to working with you.
            </p>
            <br />
            <p>
              Thanks, James
            </p>
          </div>
          <div class="margin-top--double">
            <div class="logo-icon__container logo-icon__container--show-mobile">
              <a href="https://github.com/trenholme90" class="logo-icon logo-icon--large">
                <Github />
              </a>
              <a href="https://www.linkedin.com/in/james-trenholme-586839111/" class="logo-icon logo-icon--large">
                <LinkedIn />
              </a>
              <a href="mailto:jje.trenholme@gmail.com" class="logo-icon logo-icon--large">
                <Email/>
              </a>
            </div>
          </div>
        </div>
      </section>
      <div class="section--hero__img section--hero__img-alt"></div>
    </div>
  </div>
</template>

<script>
import Github from "../components/icons/Github.vue";
import LinkedIn from "../components/icons/LinkedIn.vue";
import Email from "../components/icons/Email.vue";
export default {
  name: "contact",
  components: {
    Github,
    LinkedIn,
    Email
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
};
</script>
