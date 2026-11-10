<script setup>
import RegistrationPage from './pages/RegistrationPage.vue'
</script>
<template>
  <main class="page-shell">
    <section class="intro-panel" aria-labelledby="intro-title">
      <div class="brand-mark" aria-hidden="true">N</div>
      <p class="eyebrow">NOVA · WORKSPACE</p>
      <h1 id="intro-title">Пространство для больших идей.</h1>
      <p class="intro-copy">
        Создайте аккаунт, чтобы собирать проекты, делиться ими с командой и видеть,
        как ваши идеи становятся реальностью.
      </p>
      <div class="quote-card">
        <span class="quote-stars" aria-hidden="true">✳</span>
        <p>«Лучшие результаты начинаются с простого шага.»</p>
        <span class="quote-caption">Ваш следующий шаг — здесь</span>
      </div>
      <span class="decor decor-one" aria-hidden="true"></span>
      <span class="decor decor-two" aria-hidden="true"></span>
    </section>

    <section class="form-panel" aria-labelledby="registration-title">
      <div class="form-topline"><span>Уже есть аккаунт?</span> <a href="#login">Войти</a></div>
      <div class="form-content">
        <p class="eyebrow">НАЧНИТЕ БЕСПЛАТНО</p>
        <h2 id="registration-title">Создать аккаунт</h2>
        <p class="form-subtitle">Заполните форму, чтобы присоединиться к Nova.</p>
        <RegistrationPage />
      </div>
      <p class="legal-note">Продолжая, вы соглашаетесь с условиями использования и политикой конфиденциальности.</p>
    </section>
  </main>
</template>
