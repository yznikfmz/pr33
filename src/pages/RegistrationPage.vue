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

const touched = reactive({
  name: false,
  email: false,
  password: false,
  confirmPassword: false,
})

const passwordPattern =
  /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]).{8,}$/

const submitted = ref(false)
const successMessage = ref('')

function validateField(field) {
  if (field === 'name') {
    errors.name =
      form.name.trim().length < 2
        ? 'Имя должно содержать не менее 2 символов.'
        : ''
  }

  if (field === 'email') {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    errors.email = emailPattern.test(form.email)
      ? ''
      : 'Введите корректный email.'
  }

  if (field === 'password') {
    errors.password = passwordPattern.test(form.password)
      ? ''
      : 'Нужно минимум 8 символов: строчная и заглавная буквы, цифра и спецсимвол.'

    if (touched.confirmPassword) {
      validateField('confirmPassword')
    }
  }

  if (field === 'confirmPassword') {
    errors.confirmPassword =
      form.confirmPassword && form.password === form.confirmPassword
        ? ''
        : 'Пароли должны совпадать.'
  }
}

function touchAndValidate(field) {
  touched[field] = true
  successMessage.value = ''
  validateField(field)
}

function validate() {
  for (const field of Object.keys(touched)) {
    touched[field] = true
    validateField(field)
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
        @input="touchAndValidate('name')"
        @blur="touchAndValidate('name')"
        class="form-input"
        type="text"
        :class="{ 'input-error': (submitted || touched.name) && errors.name }"
      />
      <span v-if="(submitted || touched.name) && errors.name" class="error-message">
        {{ errors.name }}
      </span>
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input
        id="email"
        v-model="form.email"
        @input="touchAndValidate('email')"
        @blur="touchAndValidate('email')"
        class="form-input"
        type="email"
        :class="{ 'input-error': (submitted || touched.email) && errors.email }"
      />
      <span v-if="(submitted || touched.email) && errors.email" class="error-message">
        {{ errors.email }}
      </span>
    </div>

    <div class="form-group">
  <label for="password">Пароль</label>
  <input
    id="password"
    v-model="form.password"
    @input="touchAndValidate('password')"
    @blur="touchAndValidate('password')"
    class="form-input"
    type="password"
    :class="{ 'input-error': (submitted || touched.password) && errors.password }"
  />
  <span
    v-if="(submitted || touched.password) && errors.password"
    class="error-message"
  >
    {{ errors.password }}
  </span>
</div>

    <div class="form-group">
  <label for="confirmPassword">Подтверждение пароля</label>
  <input
    id="confirmPassword"
    v-model="form.confirmPassword"
    @input="touchAndValidate('confirmPassword')"
    @blur="touchAndValidate('confirmPassword')"
    class="form-input"
    type="password"
    :class="{ 'input-error': (submitted || touched.confirmPassword) && errors.confirmPassword }"
  />
  <span
    v-if="(submitted || touched.confirmPassword) && errors.confirmPassword"
    class="error-message"
  >
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