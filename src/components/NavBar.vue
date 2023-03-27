<script setup>
import { onMounted, onUnmounted, ref, watchEffect } from 'vue'
import logoSrc from '@/assets/img/logo.svg'
import logoSmall from '@/assets/img/logo-small.svg'

const scrolledNav = ref(null)
const mobile = ref(null)
const mobileNav = ref(null)
const windowWidth = ref(window.innerWidth)
const show = ref(false)

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

    const timer = setInterval(() => {
      show.value = true
      clearInterval(timer)
    }, 300)
  } else {
    scrolledNav.value = false
    const timer = setInterval(() => {
      show.value = false
      clearInterval(timer)
    }, 300)
  }
}

const handleLogoHover = () => {
  scrolledNav.value = !scrolledNav.value
  const timer = setInterval(() => {
    show.value = false
    clearInterval(timer)
  }, 300)
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
    <transition name="fade">
      <nav class="nav" v-if="!scrolledNav && !show">
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
          <div class="dropdown-nav" v-show="mobileNav">
            <div class="mobile-nav-icon" v-show="mobileNav">
              <img class="mobile-nav-icon__logo" :src="logoSmall" alt="altLogo" />
              <img
                class="mobile-nav-icon__toggle-close"
                @click="toggleMobileNav"
                src="@/assets/img/nav/toggle-close.svg"
                alt=""
              />
            </div>

            <h2 class="dropdown-nav__link">La pépinière</h2>
            <h2 class="dropdown-nav__link">La carte</h2>
            <h2 class="dropdown-nav__link">Notre histoire</h2>
            <h2 class="dropdown-nav__link">L’équipe</h2>
            <h2 class="dropdown-nav__link">Inspiration</h2>
          </div>
        </transition>
      </nav>
      <div class="logo" v-else-if="scrolledNav && show" @mouseover="handleLogoHover">
        <img :src="logoSmall" alt="" />
      </div>
    </transition>
  </header>
</template>

<style scoped lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-leave,
.fade-enter-from {
  opacity: 0;
}
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
      background-color: var(--color-emeraude);
      &__link {
        color: var(--color-cream);
        list-style: none;
      }
    }
  }
  .mobile-nav-enter-active,
  .mobile-nav-leave-active {
    transition: 1s ease all;
  }

  .mobile-nav-enter-from,
  .mobile-nav-leave-to {
    transform: translateX(100%);
  }

  .mobile-nav-enter-to {
    transform: translateX(0);
  }

  .mobile-nav-icon {
    z-index: 999;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 5rem;
    &__logo {
      background-color: rgba(245, 245, 245, 0.9);
      border-radius: 220px;
      padding: 1rem 2rem;
      position: fixed;
      left: 50%;
      top: 2rem;
      transform: translateX(-50%);
    }

    &__toggle-close {
      position: fixed;
      top: 2rem;

      left: 100%;
      transform: translateX(-100%);
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

