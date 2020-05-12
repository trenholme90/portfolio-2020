<template>
  <nav class="nav">
    <router-link to="/" data-page="home">
      <Logo logo-class="header__logo" />
    </router-link>
    <div class="menu" :class="{ 'is-open': isOpen }">
      <ul class="menu__list">
        <div class="menu__inner">
          <router-link to="/work/Jet2" class="menu__item" data-page="work">
            Work
          </router-link>
          <router-link to="/contact" class="menu__item" data-page="contact">
            Contact
          </router-link>
        </div>
        <div class="menu__item logo-icon__container">
          <a href="https://github.com/trenholme90" class="logo-icon">
            <Github />
          </a>
          <a href="https://www.linkedin.com/in/james-trenholme-586839111/" class="logo-icon">
            <LinkedIn />
          </a>
          <a href="mailto:jje.trenholme@gmail.com" class="logo-icon">
            <Email/>
          </a>
        </div>
      </ul>
    </div>
    <Hamburger
      :menuIsOpen="isOpen"
      @click.native="toggleMenu"
      class="hide-desktop"
    />
  </nav>
</template>

<script>
import Logo from "./Logo.vue";
import Hamburger from "./icons/Hamburger.vue";
import Github from "./icons/Github.vue";
import LinkedIn from "./icons/LinkedIn.vue";
import Email from "./icons/Email.vue";
export default {
  name: "Nav",
  components: {
    Logo,
    Hamburger,
    Github,
    LinkedIn,
    Email
  },
  data: () => {
    return {
      isOpen: false
    };
  },
  watch: {
    $route() {
      this.isOpen = false;
    }
  },
  methods: {
    toggleMenu: function() {
      this.isOpen ? (this.isOpen = false) : (this.isOpen = true);
    }
  }
};
</script>
