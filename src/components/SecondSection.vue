<script setup>
import planteImg from '@/assets/img/second-section/plante.svg'
import coffeeImg from '@/assets/img/second-section/coffee.svg'

import { ref } from 'vue'

const images = [
  {
    id: 0,
    src: planteImg,
    alt: 'Image 1'
  },
  {
    id: 1,
    src: coffeeImg,
    alt: 'Image 2'
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

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
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



