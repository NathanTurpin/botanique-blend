<script setup>
import NavBar from './NavBar.vue'
</script>

<template>
  <header class="hero">
    <NavBar />
    <div class="hero-banner">
      <div class="hero-banner__left">
        <h1>Coffee Addict and Plant Lover, Botanic Blend est fait pour toi,</h1>

        <div class="hero-banner__actions">
          <button>Découvrir les plantes</button>

          <button>Voir la carte</button>
        </div>
      </div>

      <div class="hero-banner__right">
        <img class="hero-banner__left-small" src="@/assets/img/header/img-left-small.svg" alt="" />
        <img class="hero-banner__rec-fond" src="@/assets/img/header/rec-fond.svg" alt="" />
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
  // background-color: red;
}

.hero-banner {
  height: 90%;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 1fr;
  grid-column-gap: 0px;
  position: absolute;
  grid-row-gap: 0px;
  margin-top: 8vh;
  &__left {
    grid-area: 1 / 1 / 2 / 2;
  }
  &__right {
    grid-area: 1 / 2 / 2 / 3;
    position: relative;
  }

  &__rec-fond {
    position: absolute;
    top: 2%;
    left: 0;
    width: 100%;
    height: 100%;
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
    width: 19%;
    top: 36%;
    left: 38%;
    z-index: 9;
  }

  &__img-right {
    position: absolute;
    top: 40%;
    left: 52%;
    width: 42%;
  }
}
</style>