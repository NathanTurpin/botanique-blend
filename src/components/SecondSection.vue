<script setup>
import planteImg from '@/assets/img/second-section/plante.svg'
import coffeeImg from '@/assets/img/second-section/coffee.svg'
import feuilleImg from '@/assets/img/second-section/feuille.svg'

import { ref } from 'vue'

const images = [
  {
    id: 0,
    src: planteImg,
    alt: 'Image 1',
    title: 'Cold Brew Latte',
    text: 'Laissez-vous envoûter par notre Cold Brew Latte, un mariage subtil entre la fraîcheur glacée et la douceur onctueuse, pour une expérience de dégustation inoubliable',
    btns: ['voir la carte']
  },
  {
    id: 1,
    src: coffeeImg,
    alt: 'Image 2',
    title: 'Oiseau du Paradis',
    text: "l'Oiseau du Paradis, un véritable chef-d'œuvre de la nature, qui vous invite à explorer un monde de couleurs vives et de formes majestueuses",
    btns: ['découvrir', "télécharger le guide d'entretien"]
  }
]

const imageOrder = ref([0, 1])

const orderedImages = imageOrder.value.map((order) => images[order])

const swapImages = () => {
  imageOrder.value = [imageOrder.value[1], imageOrder.value[0]]
}
</script> 

<template>
  <section class="second-section">
    <div class="left-section">
      <img :src="feuilleImg" alt="" class="left-section__feuille" />
      <div class="content">
        <span class="content__span label label--small">notre duo du mois</span>

        <div class="content__buttons">
          <button @click="swapImages" class="content__buttons--left">Swap</button>

          <button @click="swapImages" class="content__buttons--right">Swap</button>
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

            <div class="content__infos-btns" v-for="(btn, index) in image.btns" :key="index">
              <button>{{ btn }}</button>
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
</template>

<style lang="scss" scoped>
.second-section {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  height: 100vh;
}

.left-section {
  flex: 1;
  position: relative;

  &__feuille {
    width: 60%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -99;
  }
  .body {
    text-align: left;
  }
  .content {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: flex-end;
    gap: 1rem;
    height: 52%;
    width: 90%;
    margin: auto;

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

    &__buttons {
      background-color: #f2f2f2;
      border: none;
      cursor: pointer;
      padding: 0.5rem;
      border-radius: 4px;
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
</style>



