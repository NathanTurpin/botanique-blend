<script setup>
import { onMounted, onUnmounted, ref, watchEffect } from 'vue'
import logoSrc from '@/assets/img/logo.svg'
import logoSmall from '@/assets/img/logo-small.svg'

const scrolledNav = ref(null)
const mobile = ref(null)
const mobileNav = ref(null)
const windowWidth = ref(window.innerWidth)

const toggleMobileNav = () => {
  mobileNav.value = !mobileNav.value
}

watchEffect(() => {
  if (windowWidth.value <= 1026) {
    mobile.value = true
  } else {
    mobileNav.value = false
    mobile.value = false
  }
})

const handleScroll = () => {
  if (window.pageYOffset > 0) {
    scrolledNav.value = true

    return
  }
  scrolledNav.value = false
}

const handleLogoHover = () => {
  scrolledNav.value = !scrolledNav.value
}

window.addEventListener('resize', () => {
  windowWidth.value = window.innerWidth
})

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header class="container">
    <nav class="nav" v-if="!scrolledNav">
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
    <div class="logo" v-else @mouseover="handleLogoHover">
      <img :src="logoSmall" alt="" />
    </div>
  </header>
</template>

<style scoped lang="scss">
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 99;
  transition: all 0.5s ease-in-out;

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

  .logo {
    width: 10%;
    margin: 1rem auto;
    background-color: rgba(245, 245, 245, 0.9);
    border-radius: 220px;
    padding: 1rem 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>

