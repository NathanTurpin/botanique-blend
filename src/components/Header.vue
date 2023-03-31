<script setup>
import LaurTop from '@/assets/img/header/laur-top.svg'
import LaurBottom from '@/assets/img/header/laur-bottom.svg'
import ImgLeftSmall from '@/assets/img/header/img-left-small.svg'
import ImgLeftGrande from '@/assets/img/header/img-left-grande.svg'
import ImgMid from '@/assets/img/header/img-mid.svg'
import ImgRight from '@/assets/img/header/img-right.svg'

import NavBar from './NavBar.vue'
import useWindowSize from '../assets/composables/useWindowSize'
import { ref, watchEffect } from 'vue'

const { width } = useWindowSize()
const isMobile = ref(null)

watchEffect(() => {
  if (width.value <= 1026) {
    isMobile.value = true
  } else {
    isMobile.value = false
  }
})
</script>

<template>
  <header class="hero">
    <NavBar />
    <div class="hero-banner" v-if="!isMobile">
      <div class="hero-banner__left">
        <img class="hero-banner__laur-top" :src="LaurTop" alt="" />
        <img class="hero-banner__laur-bottom" :src="LaurBottom" alt="" />
        <h1 class="hero-banner__title">
          Coffee Addict and Plant Lover, Botanic Blend est fait <br />
          pour toi,
        </h1>

        <div class="hero-banner__actions">
          <button class="buttons buttons__emeraude">Découvrir les plantes</button>

          <button class="buttons buttons__coffee--outlined">Voir la carte</button>
        </div>
      </div>

      <div class="hero-banner__right">
        <div class="hero-banner__rec-fond"></div>
        <img class="hero-banner__left-small" :src="ImgLeftSmall" alt="" />
        <img class="hero-banner__left-grande" :src="ImgLeftGrande" alt="" />
        <img class="hero-banner__mid" :src="ImgMid" alt="" />
        <img class="hero-banner__img-right" :src="ImgRight" alt="" />
      </div>
    </div>

    <div class="hero-mobile" v-else>
      <div class="hero-mobile__image-container">
        <!-- <img :src="ImgLeftGrande" alt="" class="hero-mobile__image" /> -->
      </div>

      <div class="hero-mobile__content">
        <h2 class="hero-mobile__title">
          Coffee Addict and Plant Lover, Botanic Blend est fait <br />
          pour toi,
        </h2>

        <div class="hero-mobile__actions">
          <button class="buttons buttons__coffee--outlined">Découvrir les plantes</button>

          <button class="buttons buttons__emeraude">Voir la carte</button>
        </div>
      </div>
    </div>
  </header>
</template>


<style lang="scss" scoped>
.hero {
  background-image: url('@/assets/img/header/coffee-bean.svg');
  height: 100vh;
  width: 100%;
  background-size: cover;
  background-position: center;
  background-color: var(--color-cream);
}

.hero-banner {
  height: 100%;
  display: grid;
  grid-template-columns: minmax(0, 56vw) minmax(0, 40vw);

  &__left {
    position: relative;
    grid-area: 1 / 1 / 2 / 2;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
  }

  &__laur-top {
    position: absolute;
    top: -4%;
    left: 0;
    width: 54vh;
  }
  &__laur-bottom {
    position: absolute;
    top: 53%;
    left: 0;
    width: 35vh;
  }
  &__title {
    width: 70%;
    color: var(--color-emeraude);
    z-index: 99;
  }

  &__actions {
    display: flex;
    flex-direction: row;
    gap: 0.2rem;
    width: 70%;
    z-index: 99;
  }

  &__right {
    grid-area: 1 / 2 / 2 / 3;
    position: relative;
  }

  &__rec-fond {
    background-image: url('@/assets/img/header/rec-fond.svg');
    height: 100%;
    background-position: bottom;
    background-size: cover;
    background-repeat: no-repeat;
    width: 42.8vw;
  }

  &__left-small {
    position: absolute;
    z-index: 9;
    width: 25%;
    height: auto;
    top: 45%;
    left: -22%;
  }

  &__left-grande {
    top: 7%;
    left: -5%;
    width: 29vw;
    height: 100vh;
    position: absolute;
  }

  &__mid {
    position: absolute;
    width: 12vw;
    top: 33%;
    left: 49%;
    z-index: 9;
  }

  &__img-right {
    position: absolute;
    top: 50%;
    left: 69%;
    width: 15vw;
  }
}

.hero-mobile {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  &__image-container {
    background-image: url('@/assets/img/header/img-left-grande.svg');
    height: 100%;
    width: 100%;
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  &__content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem; /* Ajustez l'espace entre les éléments ici */
    text-align: center;
    margin: 1rem;
  }
  &__title {
    color: var(--color-emeraude);
  }

  &__actions {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
  }
}
</style>