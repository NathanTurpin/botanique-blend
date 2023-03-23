<script setup>
import { ref, watchEffect } from 'vue'
import logoSrc from '@/assets/img/logo.svg'
const showMenu = ref(false)
const fullscreenMenu = ref(false)
const screenWidth = ref(window.innerWidth)

watchEffect(() => {
  if (screenWidth.value <= 1026 && showMenu.value) {
    fullscreenMenu.value = true
  } else {
    fullscreenMenu.value = false
  }
})

window.addEventListener('resize', () => {
  screenWidth.value = window.innerWidth
})
</script>

<template>
  <nav class="nav">
    <img :src="logoSrc" alt="altLogo" class="nav__img" />

    <ul
      class="nav__ul"
      :class="{
        'nav__ul--show': showMenu,
        'nav__ul--fullscreen': fullscreenMenu
      }"
    >
      <li class="nav__li label label--small">La pépinière</li>
      <li class="nav__li label label--small">La carte</li>
      <li class="nav__li label label--small">Notre histoire</li>
      <li class="nav__li label label--small">L’équipe</li>
      <li class="nav__li label label--small">inspiration</li>
    </ul>

    <div class="nav__toggle" @click="showMenu = !showMenu" v-if="screenWidth <= 1026">
      <img
        src="@/assets/img/nav/toggle.svg"
        :class="{ 'nav__toggle-icon--open': showMenu }"
        alt=""
      />
    </div>
  </nav>
</template>

<style scoped lang="scss">
.nav {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 80%;
  margin: 1rem auto;
  background-color: rgba(245, 245, 245, 0.9);
  border-radius: 220px;
  padding: 1rem 2rem;

  &__img {
    width: 5rem;
  }
  &__toggle {
    align-items: center;
    justify-content: center;
    width: 2rem;
    height: 2rem;
    cursor: pointer;

    &-icon--open {
      transform: rotate(90deg);
    }
  }
  &__ul {
    display: flex;
    flex-direction: row;
    gap: 2rem;
    list-style: none;
    align-items: center;

    &--show {
      display: flex;
    }

    &--fullscreen {
      background-color: rgba(245, 245, 245, 0.9);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 999;
    }
  }
  &__li {
    color: var(--color-emeraude);
  }
}
</style>

