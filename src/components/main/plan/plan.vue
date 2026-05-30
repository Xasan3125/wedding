<template>
  <div
      class="relative flex flex-col justify-center items-center min-h-screen bg-cover bg-center bg-no-repeat"
      :style="{ backgroundImage: `url('/image-bg.jpg')` }"
  >
    <!-- Затемнение фона (опционально, для лучшей читаемости) -->
    <div class="absolute inset-0 bg-black/30"></div>

    <div class="relative z-10 p-4 md:p-10 bg-white/95 backdrop-blur-sm rounded-xl shadow-lg max-w-2xl m-4">
      <h2 class="font-bold text-sm md:text-lg text-center mb-4 text-black/50">ПРИГЛАШЕНИЕ</h2>
      <p class="text-center text-2xl md:text-6xl text-black mb-8">24 июля</p>

      <div>
        <div v-for="(item, index) in schedule" :key="index" class="text-center mb-10">
          <p class="text-lg md:text-2xl font-semibold text-black/50 mb-1">
            — {{ item.time }} —
          </p>
          <h3 class="text-sm md:text-2xl font-bold text-black mb-2">{{ item.title }}</h3>
          <p class="text-sm md:text-2xl text-black/50">{{ item.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const schedule = ref([
  {
    time: '17:00',
    title: 'Сбор гостей, фуршет',
    description: 'Собираясь на мероприятие, просим взять с собой ваши прекрасные улыбки и хорошее настроение!'
  },
  {
    time: '17:30',
    title: 'Церемония бракосочетания',
    description: 'На всякий случай приготовьте платочки для трогательного момента!'
  },
  {
    time: '18:00',
    title: 'Начало банкета',
    description: 'Время вкусной еды, танцев и развлечений!'
  },
  {
    time: '21:00',
    title: 'Свадебный торт',
    description: 'Сладкая традиция которую мы не можем обойти стороной.'
  },
  {
    time: '23:00',
    title: 'Окончание вечера',
    description: 'К сожалению, даже такой прекрасный вечер может закончиться.'
  }
])
</script>

<style scoped>
</style>