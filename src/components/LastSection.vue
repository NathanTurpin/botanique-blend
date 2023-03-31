  <script setup>
import { ref } from 'vue'
import Epi1 from '@/assets/img/last-section/epi1.svg'
import Epi2 from '@/assets/img/last-section/epi2.svg'
import Epi3 from '@/assets/img/last-section/epi3.svg'
import Epi4 from '@/assets/img/last-section/epi4.svg'
const comments = ref([
  {
    id: 0,
    hour: '17.02',
    name: 'marie-louise',
    desc: 'Botanic Blend est un vrai bijou caché dans la ville. Les baristas sont compétents et sympathiques, et les plantes donnent une atmosphère apaisante. Je recommande vivement cet endroit !'
  },
  {
    id: 1,
    hour: '14.02',
    name: 'seb',
    desc: "Le choix de plantes chez Botanic Blend est impressionnant ! J'ai trouvé toutes les plantes que je cherchais, et plus encore. Le personnel était très serviable et m'a donné des conseils d'entretien."
  },
  {
    id: 2,
    hour: '12.02',
    name: 'léonie',
    desc: "J'adore l'ambiance de ce magasin ! Il est facile de passer des heures à explorer tous les coins et recoins de cette oasis verte. Le personnel est super accueillant et connaît tout sur les plantes."
  }
])
</script>
<template>
  <section class="last-section">
    <div class="last-section__contain">
      <h2 class="last-section__header">Vos derniers mots doux</h2>
      <div class="last-section__container">
        <img :src="Epi1" alt="" class="last-section__epi1" />
        <img :src="Epi2" alt="" class="last-section__epi2" />
        <img :src="Epi3" alt="" class="last-section__epi3" />
        <img :src="Epi4" alt="" class="last-section__epi4" />

        <div class="last-section__block" v-for="comment in comments" :key="comment.id">
          <h2 class="last-section__title label label--small">{{ comment.hour }}</h2>
          <h3 class="last-section__subtitle label label--small">{{ comment.name }}</h3>
          <p class="last-section__description body body--large">{{ comment.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>


<style lang="scss" scoped>
.last-section {
  &__contain {
    width: 90%;
    margin: 3rem auto;
    padding: 1rem;
  }
  &__header {
    text-align: left;
    margin-bottom: 3rem;
  }

  &__container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 1rem;
    position: relative;
  }
  &__epi1 {
    position: absolute;
    top: 19%;
    width: 5%;
    left: -1%;
  }
  &__epi2 {
    position: absolute;
    top: -20%;
    width: 5%;
    left: 33%;
  }
  &__epi3 {
    position: absolute;
    top: 39%;
    width: 5%;
    left: 64%;
  }
  &__epi4 {
    position: absolute;
    top: 0;
    width: 10%;
    left: 94%;
  }
  &__block {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    flex-wrap: wrap;
    flex: 1;
    box-sizing: border-box;
    border: 1px solid var(--color-matcha);
    padding: 1rem;
  }
  &__title,
  &__subtitle {
    margin-bottom: 1rem;
    color: var(--color-matcha);
  }

  &__description {
    color: var(--color-coffee);
    width: 70%;
  }
  // @media (max-width: 768px) {
  //   &__block {
  //     min-width: calc(50% - 1rem);
  //   }
  // }

  // @media (max-width: 480px) {
  //   &__block {
  //     min-width: 100%;
  //   }
  // }
}
</style>