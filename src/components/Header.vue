<script setup>
import NavBar from './NavBar.vue'
</script>

<template>
  <header class="hero">
    <NavBar />
    <div class="hero-banner">
      <div class="hero-banner__left">
        <img class="hero-banner__laur-top" src="@/assets/img/header/laur-top.svg" alt="" />
        <img class="hero-banner__laur-bottom" src="@/assets/img/header/laur-bottom.svg" alt="" />
        <h1 class="hero-banner__title">
          Coffee Addict and Plant Lover, Botanic Blend est fait <br />
          pour toi,
        </h1>

        <div class="hero-banner__actions">
          <button>Découvrir les plantes</button>

          <button>Voir la carte</button>
        </div>
      </div>

      <div class="hero-banner__right">
        <div class="hero-banner__rec-fond"></div>
        <img class="hero-banner__left-small" src="@/assets/img/header/img-left-small.svg" alt="" />
        <img
          class="hero-banner__left-grande"
          src="@/assets/img/header/img-left-grande.svg"
          alt=""
        />
        <img class="hero-banner__mid" src="@/assets/img/header/img-mid.svg" alt="" />
        <img class="hero-banner__img-right" src="@/assets/img/header/img-right.svg" alt="" />
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
  grid-template-columns: minmax(0, 60vw) minmax(0, 40vw);

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
    top: 18%;
    left: 0;
  }
  &__laur-bottom {
    position: absolute;
    top: 53%;
    left: 0;
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

    button {
      padding: 12px 16px 12px 16px;
      font-style: normal;
      font-weight: 400;
      font-size: 16px;
      line-height: 20px;
      color: var(--color-coffee);
      border: 1px solid var(--color-coffee);
      letter-spacing: 0.04em;
      text-transform: uppercase;
      &:first-child {
        border: 1px solid var(--color-emeraude);
        background-color: var(--color-emeraude);
        color: var(--color-cream);
      }
    }
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
    width: 53%;
    height: 100%;
    position: absolute;
  }

  &__mid {
    position: absolute;
    width: 23%;
    top: 40%;
    left: 38%;
    z-index: 9;
  }

  &__img-right {
    position: absolute;
    top: 40%;
    left: 50%;
    width: 50%;
  }
}
</style>