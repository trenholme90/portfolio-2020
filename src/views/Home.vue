<template>
  <div data-page-type="home">
    <div class="page-container">
      <section class="section section--info flex--column">
        <div class="content-block content-block--center">
          <transition name="revealDown" >
            <div class="title text-block" v-show="animate">
              <transition name="revealUp" >
                <h1 v-show="animate">James Trenholme</h1>
              </transition>
            </div>
          </transition>
          <div class="margin-top margin-bottom">
            <transition name="revealDown" >
              <div class="subtitle text-block" v-show="animate">
                <transition name="revealUp" >
                  <h1 v-show="animate">Front-end Developer</h1>
                </transition>
              </div>
            </transition>
          </div>
          <transition name="fadeY" >
            <p v-show="animate">
              A front-end developer from Leeds, that helps build exciting content
              and user stories.
            </p>
          </transition>
        </div>
        <div class="flex--full-height full-width">
          <div class="flex--column flex--content-end flex-desktop--content-center">
            <footer>
              <transition name="fadeY" >
                <Button
                  btnClass="btn btn--primary"
                  btnTxt="Experience"
                  btnLink="/work/Jet2"
                  v-show="animate"
                />
              </transition>
              <transition name="fadeY" >
                <Button
                  btnClass="btn btn--secondary"
                  btnTxt="Contact"
                  btnLink="/contact"
                  v-show="animate"
                />
              </transition>
            </footer>
          </div>
        </div>
        <transition name="fadeY" >
          <div class="logo-icon__container" v-show="animate">
            <Github clss="logo-icon" />
            <Twitter clss="logo-icon" />
            <Email clss="logo-icon" />
          </div>
        </transition>
      </section>
      <transition name="FadeYLowOpacity" >
        <div class="section--hero__img" v-show="animate"></div>
      </transition>
    </div>
  </div>
</template>

<script>
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
  },
  data: function() {
    return {
      animate: false
    };
  },
  mounted() {
    this.animate = true
  },
  beforeRouteLeave (to, from, next) {
    console.log('beforeRouteLeave', to, from)
    this.animate = false
    next()
  },
  beforeDestroy() {
    console.log('beforeDestroy')
    this.animate = false
  }
};
</script>
