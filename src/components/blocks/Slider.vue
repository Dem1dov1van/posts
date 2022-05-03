<template>
  <div class="slider">
    <a-carousel autoplay>
      <div v-for="(slide, idx) in 4" :key="idx" class="slider__item">
        <h2 class="slider__title">IT-инфраструктура для бизнеса</h2>
        <p class="slider__paragraph">
          Мы предлагаем комплексные решения для всех уровней бизнеса: от
          индивидуальных предпринимателей до крупных международных компаний.
          Более 20 000 клиентов по всему миру доверяют Selectel.
        </p>
      </div>
    </a-carousel>
  </div>
</template>
