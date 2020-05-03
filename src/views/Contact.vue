<template>
  <div data-page-type="Contact">
    <div class="page-container">
      <section class="section section--info flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>Contact me</h1>
          </div>
          <div class="margin-top padding">
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
          <div class="margin-top padding">
            <div class="logo-icon__container logo-icon__container--show-mobile">
              <Github clss="logo-icon logo-icon--large" />
              <Twitter clss="logo-icon logo-icon--large" />
              <Email clss="logo-icon logo-icon--large" />
            </div>
          </div>
        </div>
      </section>
      <div class="section--hero__img section--hero__img--alt"></div>
    </div>
  </div>
</template>

<script>
import Github from "../components/icons/Github.vue";
import Twitter from "../components/icons/Twitter.vue";
import Email from "../components/icons/Email.vue";
export default {
  name: "contact",
  components: {
    Github,
    Twitter,
    Email
  }
};
</script>
