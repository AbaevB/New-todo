<!-- src/components/Header.vue -->

<script setup>
import { ref, onMounted, computed } from 'vue';
import Btn from './Btn.vue';

// Реактивное состояние темы
const theme = ref('dark');

// Вычисляем содержимое кнопки на основе состояния
const btnContent = computed(() => {
  return theme.value === 'light' ? '\u263E' : '\u2600';
});


function changeTheme() {
  const current = document.documentElement.getAttribute('data-theme');
  const newTheme = current === 'light' ? null : 'light';

  document.documentElement.setAttribute('data-theme', newTheme);
  localStorage.setItem('theme', newTheme);

  // Обновляем реактивную переменную
  theme.value = newTheme || 'dark';
}

// Восстанавливаем тему при загрузке
onMounted(() => {
  const savedTheme = localStorage.getItem('theme');
  const initialTheme = savedTheme || 'dark';
  theme.value = initialTheme;

  document.documentElement.setAttribute('data-theme', savedTheme);
});
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header__content">
        <img src="/images/logo.png" alt="TODO logo">
        <h1 class="header__title">TODO List</h1>
        <Btn
          :content="btnContent"
          btn-class="header__btn"
          btn-type="button"
          btn-aria-label="Сменить тему"
          @click="changeTheme"
        />
      </div>
    </div>
  </header>
</template>