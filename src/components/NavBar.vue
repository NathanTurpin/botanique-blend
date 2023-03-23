<script setup>
import { ref } from 'vue'
import logoSrc from '@/assets/img/logo.svg'
// const scrollPositon = ref(null)
const mobile = ref(true)
const mobileNav = ref(null)
// const windowWidth = ref(window.innerWidth)

const toggleMobileNav = () => {
  console.log(mobileNav.value)
  mobileNav.value = !mobileNav.value
}
</script>

<template>
  <header :class="{ 'scrolled-nav': scrollPosition }">
    <nav class="nav">
      <div class="nav__branding">
        <img :src="logoSrc" alt="altLogo" class="nav__logo" />
      </div>

      <ul class="nav__navigation" v-show="!mobile">
        <li class="nav__link label label--small">La pépinière</li>
        <li class="nav__link label label--small">La carte</li>
        <li class="nav__link label label--small">Notre histoire</li>
        <li class="nav__link label label--small">L’équipe</li>
        <li class="nav__link label label--small">inspiration</li>
      </ul>

      <div class="nav__icon">
        <img v-show="mobile" @click="toggleMobileNav" src="@/assets/img/nav/toggle.svg" alt="" />
      </div>

      <transition name="mobile-nav">
        <ul class="dropdown-nav" v-show="mobileNav">
          <li class="dropdown-nav__link label label--small">La pépinière</li>
          <li class="dropdown-nav__link label label--small">La carte</li>
          <li class="dropdown-nav__link label label--small">Notre histoire</li>
          <li class="dropdown-nav__link label label--small">L’équipe</li>
          <li class="dropdown-nav__link label label--small">inspiration</li>
        </ul>
      </transition>

      <transition name="mobile-nav-icon">
        <div class="dropdown-nav__icon-close" v-show="mobileNav">
          <img @click="toggleMobileNav" src="@/assets/img/nav/toggle.svg" alt="" />
        </div>
      </transition>
    </nav>
  </header>
</template>

<style scoped lang="scss">
header {
  position: fixed;
  z-index: 99;
  width: 100%;
  transition: 0.5s ease all;
}
.nav {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 80%;
  margin: 1rem auto;
  background-color: rgba(245, 245, 245, 0.9);
  border-radius: 220px;
  padding: 1rem 2rem;

  &__branding {
    display: flex;
    align-items: center;
  }

  &__logo {
    transition: 0.5 ease all;
    width: 5rem;
  }

  &__navigation {
    display: flex;
    justify-content: flex-end;
    gap: 2rem;
    list-style: none;
    align-items: center;
    flex: 1;
  }

  &__link {
    color: var(--color-emeraude);
  }

  &__icon {
    display: flex;
    align-items: center;
    height: 100%;
    cursor: pointer;
    transition: 0.8s ease all;
  }

  .dropdown-nav {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background-color: var(--color-base);
    &__link {
      color: wheat;
      list-style: none;
    }
    &__icon-close {
      background-color: white;
      z-index: 999;
    }
  }
}
</style>

