    <script setup>
import FeuilleLeft from '@/assets/img/footer/left.svg'
import FeuilleRight from '@/assets/img/footer/feuille-right.svg'
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
  <footer class="footer">
    <div class="footer__image-container">
      <img :src="FeuilleLeft" alt="" class="footer__feuille-left" />
      <div class="footer__element-wrapper">
        <div class="footer__contact">
          <p class="footer__title label label--medium">Venez nous voir ou contactez-nous</p>
          <h3 class="footer__adress">75 rue des bleuets, 59000 Lille</h3>
          <h3 class="footer__tel">+33 367-876-980</h3>
          <h4 class="footer__mail">contact@botanicblend.fr</h4>
        </div>
        <div class="footer__nav-bottom">
          <p class="caption">Mentions légales</p>
          <p class="caption">click&collect</p>
          <p class="caption">le concept</p>
          <p class="caption">rejoins-nous</p>
        </div>
      </div>
      <img :src="FeuilleRight" alt="" class="footer__feuille-right" />
    </div>
  </footer>
</template>


<style lang="scss" scoped>
.footer {
  &__image-container {
    background-image: url('@/assets/img/footer/fond-infos.svg');
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    position: relative;
    width: 100%;
    padding-bottom: 41.25%;
    overflow: hidden;
  }

  &__element-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 71%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
    padding: 1vh 0;
    margin-top: 12%;
  }
  &__feuille-left {
    position: absolute;
    bottom: -15%;
    left: 5%;
    width: 33vw;
    height: auto;
  }

  &__feuille-right {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 41vw;
    height: auto;
  }
  &__contact {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1vh;
  }

  &__title {
    font-weight: 700;
    font-size: 1.5vw;
    color: var(--color-emeraude);
    margin-bottom: 9%;
  }

  &__adress,
  &__tel,
  &__mail {
    font-size: 1.5vw;
    margin-bottom: -2vh;
  }

  &__mail {
    opacity: 0.5;
  }

  &__nav-bottom {
    display: flex;
    width: 37%;
    justify-content: space-between;
    .caption {
      font-size: 1vw;
    }
  }
}
</style>