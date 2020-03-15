<template>
  <div data-page-type="home">
    <div class="page-container">
      <section class="section section--info flex--column">
        <div class="content-block content-block--center">
          <div class="title text-block">
            <h1>James Trenholme</h1>
          </div>
          <div class="subtitle text-block">
            <h1>Front-end Developer</h1>
          </div>
          <p>
            A front-end developer from Leeds, that helps build exciting content
            and user stories.
          </p>
        </div>
        <div class="flex--full-height full-width">
          <div class="flex--column flex--content-end flex-desktop--content-center">
            <footer>
              <Button
                btnClass="btn btn--primary"
                btnTxt="Experience"
                btnLink="/work"
              />
              <Button
                btnClass="btn btn--secondary"
                btnTxt="Contact"
                btnLink="/contact"
              />
            </footer>
          </div>
        </div>
      </section>
      <div class="section--hero__img"></div>
    </div>
  </div>
</template>

<script>
import Button from "../components/Button.vue";
export default {
  name: "home",
  components: {
    Button
  }
};
</script>
