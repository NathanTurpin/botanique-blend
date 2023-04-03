  <script setup>
import { ref, watchEffect } from 'vue'
import useWindowSize from '../assets/composables/useWindowSize'
import { Swiper, SwiperSlide } from 'swiper/vue'

const { width } = useWindowSize()
const isMobile = ref(null)

watchEffect(() => {
  if (width.value <= 1026) {
    isMobile.value = true
  } else {
    isMobile.value = false
  }
})

const tabs = ref([
  {
    id: 0,
    date: '28.02',
    hour: '18',
    title: 'poterie',
    desc: "Créez une œuvre unique et laissez votre créativité s'exprimer ! Notre atelier de poterie vous permettra de découvrir cette technique millénaire et de façonner votre propre objet de décoration."
  },
  {
    id: 1,
    date: '29.02',
    hour: '18',
    title: 'yoga',
    desc: 'Relaxez votre corps et apaisez votre esprit avec notre atelier de yoga. Apprenez des postures simples et efficaces pour vous détendre et prendre soin de vous.'
  },
  {
    id: 2,
    date: '01.03',
    hour: '17',
    title: 'art latte',
    desc: 'Devenez un pro du latte art grâce à notre atelier dédié ! Découvrez les astuces des baristas experts et épatez vos amis avec vos créations originales.'
  }
])
</script>
<template>
  <section class="third-section" v-if="!isMobile">
    <div class="content">
      <div class="content__top">
        <h2>Ateliers et évènements à venir</h2>
        <button class="buttons buttons__coffee label label--small">Voir l'agenda complet</button>
      </div>
      <div class="content__bot" v-for="tab in tabs" :key="tab.id">
        <div class="content__bot-tab">
          <div class="content__time">
            <h3>{{ tab.date }}</h3>
            <h4>{{ tab.hour }}H</h4>
          </div>
          <h3 class="content__title">{{ tab.title }}</h3>
          <p class="body body--large content__desc">{{ tab.desc }}</p>
          <button class="content__btn buttons buttons__emeraude label label--xsmall">
            réserver
            <svg viewBox="0 0 36 8" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M35.3536 4.35355C35.5488 4.15829 35.5488 3.84171 35.3536 3.64645L32.1716 0.464466C31.9763 0.269204 31.6597 0.269204 31.4645 0.464466C31.2692 0.659728 31.2692 0.976311 31.4645 1.17157L34.2929 4L31.4645 6.82843C31.2692 7.02369 31.2692 7.34027 31.4645 7.53553C31.6597 7.7308 31.9763 7.7308 32.1716 7.53553L35.3536 4.35355ZM0 4.5H35V3.5H0V4.5Z"
                fill="#F5EFED"
              />
            </svg>
          </button>
        </div>
        <hr class="content__hr" />
      </div>
    </div>
  </section>

  <section class="mobile" v-else>
    <div class="mobile__header">
      <span class="mobile__title">Ateliers et évènements à venir</span>
    </div>
    <swiper :slides-per-view="1" :space-between="10" class="mobile__blocks">
      <swiper-slide class="mobile__slider" v-for="tab in tabs" :key="tab.id">
        <div class="mobile__content">
          <div class="mobile__time">
            <h3>
              <b> {{ tab.date }}</b>
            </h3>
            <h4>{{ tab.hour }}H</h4>
          </div>
          <h3 class="mobile__title">{{ tab.title }}</h3>
          <p class="body body--large mobile__desc">{{ tab.desc }}</p>
          <button class="mobile__btn buttons buttons__emeraude label label--xsmall">
            réserver
            <svg viewBox="0 0 36 8" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M35.3536 4.35355C35.5488 4.15829 35.5488 3.84171 35.3536 3.64645L32.1716 0.464466C31.9763 0.269204 31.6597 0.269204 31.4645 0.464466C31.2692 0.659728 31.2692 0.976311 31.4645 1.17157L34.2929 4L31.4645 6.82843C31.2692 7.02369 31.2692 7.34027 31.4645 7.53553C31.6597 7.7308 31.9763 7.7308 32.1716 7.53553L35.3536 4.35355ZM0 4.5H35V3.5H0V4.5Z"
                fill="#F5EFED"
              />
            </svg>
          </button>
        </div>
      </swiper-slide>
    </swiper>
    <div class="mobile__seeCalendar">
      <button class="buttons buttons__coffee label label--small">Voir l'agenda complet</button>
    </div>
  </section>
</template>


<style lang="scss" scoped>
.third-section {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .content {
    height: 80%;
    width: 100%;
    background-image: url('@/assets/img/third-section/fond.svg');
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

    &__top {
      display: flex;
      justify-content: space-between;
      width: 90%;
      margin: 3rem auto;
    }

    &__bot {
      width: 90%;
      margin: 3rem auto;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      gap: 1rem;
    }
    &__bot-tab {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    }
    &__time {
      width: 5%;
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      justify-content: center;
      h3 {
        font-family: 'Source Sans Pro';
        line-height: 40px;
        font-weight: 700;
        margin-bottom: -1rem;
      }
      h4 {
        opacity: 0.5;
        font-size: 1rem;
      }
    }
    &__title {
      width: 22%;
      display: flex;
      justify-content: center;
    }
    &__desc {
      width: 50%;
      text-align: left;
    }
    &__btn {
      width: 14%;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 1rem;
    }
    &__hr {
      width: 100%;
      border: 1px solid var(--color-coffee);
    }
  }
}

.mobile {
  background-image: url('@/assets/img/third-section/fond.svg');
  background-position: right;
  background-repeat: no-repeat;
  height: 80vh;
  width: 100vw;
  &__header {
    width: 100%;
    height: 15%;

    display: flex;
    justify-content: center;
    align-items: center;
  }
  &__title {
    font-family: 'Erotique Alternate Trial';
    font-style: normal;
    font-weight: 700;
    font-size: 22px;
    line-height: 22px;
  }
  &__blocks {
    padding: 1rem;
  }
  &__content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    margin: 2rem auto;
    border: 1px solid var(--color-coffee);
    padding: 1rem;
  }

  &__time {
    display: flex;
    flex-direction: column;
    align-items: center;
    h4 {
      opacity: 0.5;
      font-size: 1rem;
      margin-top: -0.8rem;
    }
  }

  &__btn {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    svg {
      width: 5vw;
    }
  }
  &__seeCalendar {
    width: 100%;
    height: 5%;

    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>