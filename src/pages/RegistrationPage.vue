<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
})

const errors = reactive({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
})

const submitted = ref(false)
const successMessage = ref('')

function validate() {
  errors.name = ''
  errors.email = ''
  errors.password = ''
  errors.confirmPassword = ''

  if (form.name.trim().length < 2) {
    errors.name = 'Имя должно содержать не менее 2 символов.'
  }

  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailPattern.test(form.email)) {
    errors.email = 'Введите корректный email.'
  }

  if (form.password.length < 6) {
    errors.password = 'Пароль должен содержать не менее 6 символов.'
  }

  if (!form.confirmPassword || form.password !== form.confirmPassword) {
    errors.confirmPassword = 'Пароли должны совпадать.'
  }

  return !Object.values(errors).some(Boolean)
}

function handleSubmit() {
  submitted.value = true
  successMessage.value = ''

  if (validate()) {
    successMessage.value = 'Проверка пройдена. Отправку подключим следующим шагом.'
  }
}
</script>

<template>
  <form class="registration-form" @submit.prevent="handleSubmit">
    <div class="form-group">
      <label for="name">Имя</label>
      <input
        id="name"
        v-model="form.name"
        class="form-input"
        type="text"
        :class="{ 'input-error': submitted && errors.name }"
      />
      <span v-if="submitted && errors.name" class="error-message">
        {{ errors.name }}
      </span>
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input
        id="email"
        v-model="form.email"
        class="form-input"
        type="email"
        :class="{ 'input-error': submitted && errors.email }"
      />
      <span v-if="submitted && errors.email" class="error-message">
        {{ errors.email }}
      </span>
    </div>

    <div class="form-group">
      <label for="password">Пароль</label>
      <input
        id="password"
        v-model="form.password"
        class="form-input"
        type="password"
        :class="{ 'input-error': submitted && errors.password }"
      />
      <span v-if="submitted && errors.password" class="error-message">
        {{ errors.password }}
      </span>
    </div>

    <div class="form-group">
      <label for="confirmPassword">Подтверждение пароля</label>
      <input
        id="confirmPassword"
        v-model="form.confirmPassword"
        class="form-input"
        type="password"
        :class="{ 'input-error': submitted && errors.confirmPassword }"
      />
      <span v-if="submitted && errors.confirmPassword" class="error-message">
        {{ errors.confirmPassword }}
      </span>
    </div>

    <button class="btn-submit" type="submit">
      Зарегистрироваться
    </button>

    <p v-if="successMessage" class="success-message">
      {{ successMessage }}
    </p>
  </form>
</template>