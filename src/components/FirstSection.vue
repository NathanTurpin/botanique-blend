<script setup>
import { reactive } from 'vue'
import product1Rec from '@/assets/img/first-section/product1-rec.svg'
import hover1 from '@/assets/img/first-section/hover1.svg'
import product2Rec from '@/assets/img/first-section/product2-rec.svg'
import hover2 from '@/assets/img/first-section/hover2.svg'
import product3Rec from '@/assets/img/first-section/product3-rec.svg'
import hover3 from '@/assets/img/first-section/hover3.svg'
import packaging1 from '@/assets/img/first-section/packaging1.svg'
import packaging2 from '@/assets/img/first-section/packaging2.svg'
import packaging3 from '@/assets/img/first-section/packaging3.svg'
import ArrowLeft from '@/assets/img/second-section/arrow-left.svg'
import ArrowRight from '@/assets/img/second-section/arrow-right.svg'
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
const products = [
  {
    id: 0,
    img: product1Rec,
    hoverImg: hover1,
    title: 'fleur de café',
    class: 'matcha',
    packaging: packaging1,
    text: 'Explosion de saveurs florales, légèrement sucrées et fruitées'
  },
  {
    id: 1,
    img: product2Rec,
    hoverImg: hover2,
    title: 'racine sauvage',
    class: 'coffee',
    packaging: packaging2,
    text: 'Note intenses de noisette grillée et de fruits rouges'
  },
  {
    id: 2,
    img: product3Rec,
    hoverImg: hover3,
    title: 'esprit de la forêt',
    class: 'emeraude',
    packaging: packaging3,
    text: 'Notes de cacao amer et de baies sauvages'
  }
]
const show = reactive([false, false, false])
const op = reactive([false, false, false])
const showHover = (product, index) => {
  op[index] = true
  if (product.id === index) {
    const timer = setInterval(() => {
      show[index] = true

      clearInterval(timer)
    }, 300)
  }
}

const hideHover = (index) => {
  op[index] = false
  const timer = setInterval(() => {
    show[index] = false

    clearInterval(timer)
  }, 300)
}

const activeIndex = ref(0)

const next = () => {
  console.log('cc')
  activeIndex.value = (activeIndex.value + 1) % products.length
}

const prev = () => {
  activeIndex.value = (activeIndex.value - 1 + products.length) % products.length
}
</script>


<template>
  <section class="first-section" v-if="!isMobile">
    <div class="first-section__top">
      <div class="label label--medium">Nouveau</div>

      <h3>Nos cafés en grains disponible en pré-commande</h3>
    </div>

    <div class="first-section__products">
      <div
        v-for="(product, index) in products"
        :key="product.id"
        class="first-section__product"
        @mouseover="showHover(product, index)"
        @mouseleave="hideHover(index)"
      >
        <transition name="fade">
          <template v-if="!show[index] && !op[index]">
            <img class="first-section__img" :src="product.img" alt="" key="normal" />
          </template>

          <template v-else-if="show[index] && op[index]">
            <div class="first-section__hover-container">
              <img class="first-section__img" :src="product.hoverImg" alt="" key="hover" />
              <p class="first-section__text">
                {{ product.text }}
              </p>
            </div>
          </template>
        </transition>

        <transition name="slide-fade">
          <img
            v-if="!show[index] && !op[index]"
            class="first-section__packaging"
            :src="product.packaging"
            alt=""
          />
        </transition>

        <h4 class="first-section__title">{{ product.title }}</h4>
        <div class="rectangle" :class="'rectangle--' + product.class">
          <button
            class="first-section__buttons label label--small"
            :class="'first-section__buttons--' + product.class"
          >
            pré-commander
          </button>
        </div>
      </div>
    </div>
  </section>

  <section class="mobile" v-else>
    <div class="mobile__header">
      <span class="label label--medium">Nouveau</span>

      <h3>Nos cafés en grains disponible en pré-commande</h3>
    </div>

    <div class="slider">
      <div class="slider__content">
        <div
          v-for="product in products"
          :key="product.id"
          :class="{ slider__item: true, active: activeIndex === product.id }"
        >
          <img :src="product.img" :alt="product.title" class="slider__image" />
          <h4>{{ product.title }}</h4>
          <div class="rectangle" :class="'rectangle--' + product.class">
            <button
              class="first-section__buttons label label--small"
              :class="'first-section__buttons--' + product.class"
            >
              pré-commander
            </button>
          </div>
          <div class="slider__actions">
            <img :src="ArrowLeft" @click="prev" alt="" />
            <img :src="ArrowRight" alt="" @click="next" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>


<style lang="scss" scoped>
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

.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}
.first-section {
  height: 100vh;
  width: 90%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5rem;
  margin: auto;

  &__top {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  &__products {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  &__product {
    width: 32%;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    position: relative;
  }

  &__packaging {
    position: absolute;
    top: 3rem;
    width: 100%;
  }
  &__hover-container {
    position: relative;
    display: inline-block;
  }
  &__text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: var(--color-cream); // Changer la couleur du texte si nécessaire
    text-align: center;
  }
  &__img {
    width: 100%;
    height: auto;
  }

  &__title {
    margin-top: 2rem;
  }

  &__buttons {
    width: 100%;
    cursor: pointer;
    padding: 0.5rem;
    color: var(--color-white);

    &--emeraude {
      border: 1px solid var(--color-emeraude);
      background-color: var(--color-emeraude);
    }
    &--matcha {
      border: 1px solid var(--color-matcha);
      background-color: var(--color-matcha);
    }
    &--coffee {
      border: 1px solid var(--color-coffee);
      background-color: var(--color-coffee);
    }
  }
}
.rectangle {
  padding: 0.5rem;
  display: inline-block;

  &--emeraude {
    border: 0.1rem solid var(--color-emeraude);
  }

  &--coffee {
    border: 0.1rem solid var(--color-coffee);
  }

  &--matcha {
    border: 0.1rem solid var(--color-matcha);
  }
}
.mobile {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 2rem;

  &__header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0.4rem;
    height: 15%;
    h3 {
      text-align: center;
    }
  }
}

.slider {
  position: relative;
  width: 100vw;
  height: 85%;
  &__content {
    width: 100%;
    height: 100%;
  }
  &__actions {
    display: flex;
    justify-content: space-evenly;
    width: 50%;
    margin: auto;
    z-index: 999;
  }
  &__item {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.5s;
    gap: 2rem;
  }
  &__image {
    width: calc(100% - 2rem); /* Laisser un espace de 1rem (16px) de chaque côté */
    height: auto; /* Conserver les proportions de l'image */
    max-height: calc(100vh - 19rem); /* Laisser un espace de 2rem (32px) en haut et en bas */
    object-fit: contain; /* Redimensionner l'image pour qu'elle s'adapte à l'espace disponible */
  }
}
.active {
  opacity: 1;
}
</style>