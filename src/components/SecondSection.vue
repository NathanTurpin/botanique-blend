<script setup>
import planteImg from '@/assets/img/second-section/plante.svg'
import coffeeImg from '@/assets/img/second-section/coffee.svg'
import feuilleImg from '@/assets/img/second-section/feuille.svg'
import arrowLeft from '@/assets/img/second-section/arrow-left.svg'
import arrowRight from '@/assets/img/second-section/arrow-right.svg'
import useWindowSize from '../assets/composables/useWindowSize'
import { Swiper, SwiperSlide } from 'swiper/vue'

import { ref, watchEffect } from 'vue'

const { width } = useWindowSize()
const isMobile = ref(null)
const currentIndex = ref(0)

watchEffect(() => {
  if (width.value <= 1026) {
    isMobile.value = true
  } else {
    isMobile.value = false
  }
})
const isButtonDisabled = ref([false, false])
const images = [
  {
    id: 0,
    src: planteImg,
    alt: 'Image 1',
    title: 'Cold Brew Latte',
    text: 'Laissez-vous envoûter par notre Cold Brew Latte, un mariage subtil entre la fraîcheur glacée et la douceur onctueuse, pour une expérience de dégustation inoubliable',
    btns: [{ text: 'voir la carte', class: false }]
  },
  {
    id: 1,
    src: coffeeImg,
    alt: 'Image 2',
    title: 'Oiseau du Paradis',
    text: "l'Oiseau du Paradis, un véritable chef-d'œuvre de la nature, qui vous invite à explorer un monde de couleurs vives et de formes majestueuses",
    btns: [
      { text: 'découvrir', class: false },
      { text: "télécharger le guide d'entretien", class: true }
    ]
  }
]

const imageOrder = ref([0, 1])

const orderedImages = imageOrder.value.map((order) => images[order])

const swapImages = (index) => {
  imageOrder.value = [imageOrder.value[1], imageOrder.value[0]]
  isButtonDisabled.value[index] = true
  isButtonDisabled.value[1 - index] = false
}

const updateCurrentIndex = (swipper) => {
  currentIndex.value = swipper.activeIndex
}
</script> 

<template>
  <section class="second-section" v-if="!isMobile">
    <div class="left-section">
      <img :src="feuilleImg" alt="" class="left-section__feuille" />
      <div class="content">
        <span class="content__span label label--small">notre duo du mois</span>

        <div class="content__buttons">
          <button
            @click="swapImages(0)"
            class="content__buttons--left"
            :disabled="isButtonDisabled[0]"
          >
            <img :src="arrowLeft" alt="" />
          </button>

          <button
            @click="swapImages(1)"
            class="content__buttons--right"
            :disabled="isButtonDisabled[1]"
          >
            <img :src="arrowRight" alt="" />
          </button>
        </div>

        <div
          class="content__infos"
          v-for="(image, index) in orderedImages"
          :key="index"
          :style="{
            zIndex: imageOrder[index] === 0 ? 2 : 1,
            opacity: imageOrder[index] === 0 ? 1 : 0
          }"
        >
          <div class="content__info">
            <h2>{{ image.title }}</h2>

            <p class="body body--large">{{ image.text }}</p>

            <div class="content__infos-btns">
              <button
                v-for="(btn, index) in image.btns"
                :key="index"
                class="buttons label label--small"
                :class="btn.class ? 'buttons__emeraude--outlined' : 'buttons__emeraude'"
              >
                {{ btn.text }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="right-section">
      <div
        v-for="(image, index) in orderedImages"
        :key="image.id"
        class="image-wrapper"
        :style="{
          zIndex: imageOrder[index] === 0 ? 2 : 1,
          transform: `translateX(${imageOrder[index] * 100}%) scale(${
            imageOrder[index] === 0 ? 1.1 : 1
          }`
        }"
      >
        <img :src="image.src" :alt="image.alt" />
      </div>
    </div>
  </section>

  <!-- <section class="mobile" v-else>
    <div class="mobile__images-container">
      <img :src="planteImg" alt="" />
      <img :src="coffeeImg" alt="" />
    </div>
    <div class="mobile__content" v-for="image in images" :key="image.id">
      <h2>{{ image.title }}</h2>

      <p class="body body--large">{{ image.text }}</p>

      <div class="mobile__infos-btns">
        <button
          v-for="(btn, index) in image.btns"
          :key="index"
          class="buttons label label--small"
          :class="btn.class ? 'buttons__emeraude--outlined' : 'buttons__emeraude'"
        >
          {{ btn.text }}
        </button>
      </div>
    </div>
  </section> -->
  <section class="mobile" v-else>
    <swiper :slides-per-view="1" :space-between="10" @slideChange="updateCurrentIndex">
      <swiper-slide v-for="image in images" :key="image.id">
        <div class="mobile__images-container">
          <img :src="image.src" alt="" />
        </div>
        <div class="mobile__content">
          <span class="mobile__span label label--small">notre duo du mois</span>

          <h2>{{ image.title }}</h2>
          <p class="body body--large">{{ image.text }}</p>
          <div class="mobile__infos-btns">
            <button
              v-for="(btn, index) in image.btns"
              :key="index"
              class="buttons label label--small"
              :class="btn.class ? 'buttons__emeraude--outlined' : 'buttons__emeraude'"
            >
              {{ btn.text }}
            </button>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </section>
</template>

<style lang="scss" scoped>
.second-section {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  height: 100vh;
  .left-section {
    flex: 1;
    display: flex;
    flex-direction: column;
    .body {
      text-align: left;
    }
    &__feuille {
      width: 60%;
      margin-bottom: -30%;
      z-index: -99;
    }
    .content {
      display: flex;
      flex-direction: column;
      align-items: start;
      justify-content: center;
      gap: 1rem;
      height: 100%;
      width: 90%;
      margin: auto;

      &__span {
        color: var(--color-emeraude);
      }
      &__infos {
        transition: opacity 0.5s ease;
        width: 100%;
        position: relative;
      }

      &__info {
        position: absolute;
        top: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        gap: 1rem;
      }

      &__infos-btns {
        display: flex;
        gap: 0.5rem;
      }
      &__buttons {
        display: flex;
        gap: 1rem;
        &--left,
        &--right {
          background: none;
          border: none;
          cursor: pointer;
          &:disabled {
            opacity: 0.5;
          }
        }
      }
    }
  }

  .right-section {
    flex: 1;
    overflow: hidden;
    width: 100%;
    height: 100%;
    position: relative;

    .image-wrapper {
      position: absolute;
      bottom: -7rem;
      right: 10rem;
      width: 64%;
      height: 100%;
      transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      &:last-child {
        bottom: -6rem;
        width: 59%;
      }
      img {
        width: 100%;
        height: auto;
      }
    }
  }
}

.mobile {
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;

  &__images-container {
    display: flex;
    justify-content: center;
    width: 100%;
    img {
      width: auto;
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
  }
  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    width: 90%;
    margin: 1rem auto;
  }
  &__span {
    color: var(--color-emeraude);
  }
  &__infos-btns {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
  }
}
</style>



