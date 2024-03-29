<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'TheNavbar',
  data() {
    return {
      isOpen: null,
      isMobile: null,
    }
  },
  methods: {
    toggleNavbar() {
      this.isOpen = !this.isOpen
    },
    closeNavbar() {
      if (this.isMobile) {
        this.isOpen = false
      }
      return
    },
    checkScreen() {
      if (process.browser) {
        const screenWidth = window.innerWidth

        this.isMobile = screenWidth < 768
      }
    },
  },
  created() {
    this.checkScreen()
    if (process.browser) window.addEventListener('resize', this.checkScreen)
  },
})
</script>

<template>
  <nav class="navbar container">
    <nuxt-link to="/" @click.native="closeNavbar"
      ><TheLogo class="dark"
    /></nuxt-link>

    <div class="navbar__links" v-if="isOpen | !isMobile">
      <ul class="link-list" role="list">
        <li class="link-list__item">
          <nuxt-link to="/stories" class="font-link" @click.native="closeNavbar"
            >Stories</nuxt-link
          >
        </li>
        <li class="link-list__item">
          <nuxt-link
            to="/features"
            class="font-link"
            @click.native="closeNavbar"
            >Features</nuxt-link
          >
        </li>
        <li class="link-list__item">
          <nuxt-link to="/pricing" class="font-link" @click.native="closeNavbar"
            >Pricing</nuxt-link
          >
        </li>
      </ul>
      <ButtonsNormalButton :isDark="true" @click.native="closeNavbar"
        >Get an invite</ButtonsNormalButton
      >
    </div>

    <div class="navbar__menu" v-show="isMobile">
      <button class="btn btn--icon" v-if="!isOpen" @click="toggleNavbar">
        <img src="@/static/shared/mobile/menu.svg" alt="Open the navbar" />
      </button>
      <button class="btn btn--icon" v-else @click="toggleNavbar">
        <img src="@/static/shared/mobile/close.svg" alt="Close the navbar" />
      </button>
    </div>
  </nav>
</template>

<style lang="scss">
.navbar {
  background-color: $clr-white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  height: 4.5rem;

  &__links {
    position: absolute;
    background-color: $clr-white;
    top: 100%;
    inset-inline: 0;
    padding: 2rem;

    .link-list {
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
      margin-block-end: 1.25rem;

      &::before {
        content: '';
        position: absolute;
        background-color: $clr-grey;
        inset-inline: 0;
        height: 2px;
        bottom: 0;
      }

      &__item {
        padding-block-end: 1.25rem;

        a {
          color: $clr-black;
        }
      }
    }

    .btn {
      width: 100%;
    }

    @media (min-width: $tablet) {
      position: static;
      padding: 0;
      width: 66.6%; /* 2/3 of 100% */
      display: flex;
      align-items: center;
      justify-content: space-between;

      .link-list {
        flex-direction: row;
        margin: 0;

        &::before {
          position: initial;
        }

        * + * {
          margin-left: 1rem;
        }

        &__item {
          padding: 0;
        }
      }

      .btn {
        width: initial;
      }
    }
  }
}
</style>
