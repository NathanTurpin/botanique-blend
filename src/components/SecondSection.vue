<script setup>
import planteImg from '@/assets/img/second-section/plante.svg'
import coffeeImg from '@/assets/img/second-section/coffee.svg'

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
      <div class="content">
        <span class="content__span label label--small">notre duo du mois</span>

        <div class="content__buttons">
          <button @click="swapImages" class="swap-button">Swap</button>

          <button @click="swapImages" class="swap-button">Swap</button>
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
          <div class="infos">
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
      <div class="image-container">
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

.left-section,
.right-section {
  flex: 1;
  position: relative;
  overflow: hidden;
}
.body {
  text-align: left;
}
.content {
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
  height: 100%;

  &__infos {
    position: relative;
    transition: opacity 0.5s ease;
    width: 100%;
  }
}
.infos {
  position: absolute;
  top: 0;
  left: 0;
}
.image-container {
  position: absolute;
  right: -4rem;
  top: 3rem;
  width: 90%;
  height: 100%;
  display: flex;
}

.image-wrapper {
  position: absolute;
  top: 0;
  width: 60%;
  height: 100%;
  transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  &:last-child {
    top: -3rem;
  }
  img {
    width: 100%;
    height: auto;
  }
}

.swap-button {
  margin-top: 1rem;
  background-color: #f2f2f2;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 4px;
}
</style>



