<template>
  <nav class="nav">
    <Logo logo-class="header__logo" />
    <div class="menu" :class="{ 'is-open': isOpen }">
      <ul class="menu__list">
        <div class="menu__inner">
          <router-link to="/" class="menu__item" data-page="home">
            Home
          </router-link>
          <router-link to="/about" class="menu__item" data-page="about">
            About
          </router-link>
          <router-link to="/work/Jet2" class="menu__item" data-page="work">
            Work
          </router-link>
          <router-link to="/contact" class="menu__item" data-page="contact">
            Contact
          </router-link>
        </div>
        <div class="menu__item logo-icon__container">
          <Github clss="logo-icon" />
          <Twitter clss="logo-icon" />
          <Email clss="logo-icon" />
        </div>  
      </ul>
    </div>
    <Hamburger :menuIsOpen="isOpen" @click.native="toggleMenu" class="hide-desktop"/>
  </nav>
</template>

<script>
import Logo from "./Logo.vue";
import Hamburger from "./icons/Hamburger.vue";
import Github from "./icons/Github.vue";
import Twitter from "./icons/Twitter.vue";
import Email from "./icons/Email.vue";
export default {
  name: "Nav",
  components: {
    Logo,
    Hamburger,
    Github,
    Twitter,
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
