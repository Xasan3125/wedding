<template>
  <div class="max-w-2xl mx-auto p-6 bg-white rounded-xl shadow-lg">
    <h1 class="text-3xl font-bold text-center mb-2 text-gray-800">Форма гостя</h1>
    <p class="text-center text-gray-600 mb-8">
      Просим ответить до <span class="font-semibold">1 июля</span>
    </p>

    <form
        action="https://formsubmit.co/maxim.fesan@yandex.ru"
        method="POST"
        class="space-y-8"
    >
      <!-- Скрытые настройки Formsubmit -->
      <input type="hidden" name="_subject" value="Новый ответ гостя на свадьбу!">
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_autoresponse" value="Спасибо за ваш ответ! Мы получили вашу заявку.">
      <!-- можно указать реальный URL GitHub Pages -->
      <!-- <input type="hidden" name="_next" value="https://maximfesan.github.io/название-сайта/"> -->
      <input type="hidden" name="_autoredirect" value="false">

      <!-- Блок: Гость 1 -->
      <div class="space-y-6 border border-gray-200 rounded-xl p-4 md:p-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-2">Гость 1</h2>

        <!-- Кто -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Имя и фамилия <span class="text-red-500">*</span>
          </label>
          <input
              v-model="guest1.name"
              name="guest1_name"
              type="text"
              placeholder="Ваше имя и фамилия"
              required
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none"
          />
        </div>

        <!-- Номер телефона -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Номер телефона <span class="text-red-500">*</span>
          </label>
          <input
              v-model="guest1.phone"
              name="guest1_phone"
              type="tel"
              placeholder="+7 (999) 000-00-00"
              required
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none"
          />
        </div>

        <!-- Придет ли -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Придете ли вы? <span class="text-red-500">*</span>
          </label>
          <div class="flex flex-wrap gap-4">
            <label class="flex items-center gap-2 cursor-pointer">
              <input
                  v-model="guest1.attending"
                  name="guest1_attending"
                  type="radio"
                  value="Да"
                  required
                  class="w-4 h-4 text-blue-600"
              />
              <span>Да, приду</span>
            </label>
            <label class="flex items-center gap-2 cursor-pointer">
              <input
                  v-model="guest1.attending"
                  name="guest1_attending"
                  type="radio"
                  value="Нет"
                  required
                  class="w-4 h-4 text-blue-600"
              />
              <span>Нет, не смогу</span>
            </label>
          </div>
        </div>

        <!-- Остальные поля только если гость 1 придет -->
        <template v-if="guest1.attending === 'Да'">
          <!-- Аллергии -->
          <div>
            <label class="block text-sm font-semibold text-gray-700 mb-2">
              Аллергии или ограничения в еде
            </label>
            <textarea
                v-model="guest1.allergies"
                name="guest1_allergies"
                rows="3"
                placeholder="Например: орехи, морепродукты, лактоза..."
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none resize-none"
            ></textarea>
          </div>

          <!-- Предпочтения в алкоголе -->
          <div>
            <label class="block text-sm font-semibold text-gray-700 mb-2">
              Предпочтения в алкоголе
            </label>
            <textarea
                v-model="guest1.alcohol"
                name="guest1_alcohol"
                rows="2"
                placeholder="Например: красное вино, шампанское, виски..."
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none resize-none"
            ></textarea>
          </div>

          <!-- Предпочтение в еде: рыба/мясо -->
          <div>
            <label class="block text-sm font-semibold text-gray-700 mb-2">
              Предпочтение в еде <span class="text-red-500">*</span>
            </label>
            <div class="flex flex-wrap gap-4">
              <label class="flex items-center gap-2 cursor-pointer">
                <input
                    v-model="guest1.foodPreference"
                    name="guest1_food_preference"
                    type="radio"
                    value="Мясо"
                    required
                    class="w-4 h-4 text-blue-600"
                />
                <span>Мясо</span>
              </label>
              <label class="flex items-center gap-2 cursor-pointer">
                <input
                    v-model="guest1.foodPreference"
                    name="guest1_food_preference"
                    type="radio"
                    value="Рыба"
                    required
                    class="w-4 h-4 text-blue-600"
                />
                <span>Рыба</span>
              </label>
            </div>
          </div>
        </template>
      </div>

      <!-- Вопрос: один или с кем-то -->
      <div v-if="guest1.attending === 'Да'">
        <label class="block text-sm font-semibold text-gray-700 mb-2">
          Придете одни или с кем-то?
        </label>
        <div class="flex flex-wrap gap-4">
          <label class="flex items-center gap-2 cursor-pointer">
            <input
                v-model="withGuest"
                name="with_guest"
                type="radio"
                value="Один"
                required
                class="w-4 h-4 text-blue-600"
            />
            <span>Один/а</span>
          </label>
          <label class="flex items-center gap-2 cursor-pointer">
            <input
                v-model="withGuest"
                name="with_guest"
                type="radio"
                value="С парой"
                required
                class="w-4 h-4 text-blue-600"
            />
            <span>С парой/другом</span>
          </label>
        </div>
      </div>

      <!-- Блок: Гость 2 (если не один) -->
      <div
          v-if="guest1.attending === 'Да' && withGuest === 'С парой'"
          class="space-y-6 border border-gray-200 rounded-xl p-4 md:p-6"
      >
        <h2 class="text-xl font-semibold text-gray-800 mb-2">Гость 2</h2>

        <!-- Имя гостя -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Имя и фамилия гостя <span class="text-red-500">*</span>
          </label>
          <input
              v-model="guest2.name"
              name="guest2_name"
              type="text"
              placeholder="Имя и фамилия"
              required
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none"
          />
        </div>

        <!-- Аллергии гостя -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Аллергии или ограничения в еде у гостя
          </label>
          <textarea
              v-model="guest2.allergies"
              name="guest2_allergies"
              rows="3"
              placeholder="Например: глютен, арахис..."
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none resize-none"
          ></textarea>
        </div>

        <!-- Предпочтения в алкоголе гостя -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Предпочтения в алкоголе у гостя
          </label>
          <textarea
              v-model="guest2.alcohol"
              name="guest2_alcohol"
              rows="2"
              placeholder="Например: красное вино, шампанское, виски..."
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none resize-none"
          ></textarea>
        </div>

        <!-- Предпочтение в еде гостя -->
        <div>
          <label class="block text-sm font-semibold text-gray-700 mb-2">
            Предпочтение в еде у гостя <span class="text-red-500">*</span>
          </label>
          <div class="flex flex-wrap gap-4">
            <label class="flex items-center gap-2 cursor-pointer">
              <input
                  v-model="guest2.foodPreference"
                  name="guest2_food_preference"
                  type="radio"
                  value="Мясо"
                  required
                  class="w-4 h-4 text-blue-600"
              />
              <span>Мясо</span>
            </label>
            <label class="flex items-center gap-2 cursor-pointer">
              <input
                  v-model="guest2.foodPreference"
                  name="guest2_food_preference"
                  type="radio"
                  value="Рыба"
                  required
                  class="w-4 h-4 text-blue-600"
              />
              <span>Рыба</span>
            </label>
          </div>
        </div>
      </div>

      <!-- Кнопка отправки -->
      <button
          type="submit"
          class="w-full py-3 px-6 bg-blue-600 text-white font-semibold rounded-lg hover:bg-blue-700 transition-colors"
      >
        Отправить ответ
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const guest1 = ref({
  name: '',
  phone: '',
  attending: '',
  allergies: '',
  alcohol: '',
  foodPreference: ''
})

const guest2 = ref({
  name: '',
  allergies: '',
  alcohol: '',
  foodPreference: ''
})

const withGuest = ref('')
</script>

<style scoped>
</style>