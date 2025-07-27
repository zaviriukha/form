<template>
  <div class="relative max-w-xl mx-auto mt-10 p-6 border rounded text-center">
    <h2 class="text-2xl font-bold mb-5">Форма користувача</h2>

    <div
        v-if="loading"
        class="absolute inset-0 bg-[rgba(107,114,128,0.4)] flex items-center justify-center z-10"
    >
      <v-loader />
    </div>

    <div :class="{ 'pointer-events-none opacity-50': loading }">
      <div class="grid grid-cols-2 gap-2">
        <v-input v-model="form.firstName" label="Ім'я *" />
        <v-input v-model="form.lastName" label="Прізвище *" />
        <v-input v-model="form.login" label="Логін *" />
        <v-input v-model="form.password" label="Пароль *" type="password" />
      </div>

      <h3 class="mt-4 font-semibold mb-5">Операції *</h3>
      <div class="grid grid-cols-2 gap-2 mb-4">
        <v-checkbox
            v-for="op in operations"
            :key="op"
            v-model="form.operations"
            :value="op"
        >
          {{ op }}
        </v-checkbox>
      </div>

      <h3 class="font-semibold mb-5">Головна сторінка *</h3>
      <div class="flex flex-row flex-wrap">
        <v-radio
            v-for="page in mainPages"
            :key="page"
            v-model="form.mainPage"
            :value="page"
            class="ml-3 mb-3"
        >
          {{ page }}
        </v-radio>
      </div>

      <v-checkbox v-model="form.isSecondShift" class="mb-4">
        Робітник другої зміни
      </v-checkbox>

      <div class="mt-6">
        <v-button @click="submitForm">
          Відправити
        </v-button>
      </div>
    </div>

    <p v-if="submitted" class="mt-4 text-green-600">Форма успішно надіслана!</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import VInput from "./ui/v-input.vue";
import VCheckbox from "./ui/v-checkbox.vue";
import VRadio from "./ui/v-radio.vue";
import VButton from "./ui/v-button.vue";
import VLoader from "./ui/v-loader.vue";

const form = ref({
  firstName: '',
  lastName: '',
  login: '',
  password: '',
  operations: [],
  mainPage: '',
  isSecondShift: false
})

const operations = [
  'Склад: створення',
  'Склад: оновлення',
  'Склад: переміщення',
  'Склад: видалення',
  'Категорії: створення',
  'Категорії: оновлення',
  'Категорії: видалення',
  'Характеристики: створення',
  'Характеристики: оновлення',
  'Характеристики: видалення'
]

const mainPages = ['Склад', 'Категорії', 'Характеристики', 'Продукти', 'Операції']

const loading = ref(false)
const submitted = ref(false)

const submitForm = async () => {
  if (
      !form.value.firstName ||
      !form.value.lastName ||
      !form.value.login ||
      !form.value.password ||
      form.value.operations.length === 0 ||
      !form.value.mainPage
  ) {
    alert('Будь ласка, заповніть усі обов’язкові поля.')
    return
  }

  loading.value = true
  submitted.value = false

  await new Promise(resolve => setTimeout(resolve, 2000))

  console.log('Надіслано:', form.value)

  // Очистити форму
  Object.assign(form.value, {
    firstName: '',
    lastName: '',
    login: '',
    password: '',
    operations: [],
    mainPage: '',
    isSecondShift: false
  })

  loading.value = false
  submitted.value = true
}
</script>
