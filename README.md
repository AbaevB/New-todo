# New todo

> Цель проекта - самостоятельное создание приложения TODO-List, и закрепление навыков работы с базовой сборкой **Vue**

## Создание компонента `Btn.vue`

Компонент `src/components/Btn.vue` - переиспользуемая кнопка, которой можно задавать класс, тип, и обработчик события по клику. Пример использования :

```vue
<script setup>
import Btn from './Btn.vue';
function changeTheme(){
    console.log('Change Theme');
}
</script>
<template>
  <Btn
    content = 'Сменить тему'
    btn-class="header__btn"
    btn-type="button"
    @click="changeTheme"
  />
</template>

```

## Переключение на светлую/темную тему

### Редактирование CSS переменных для цветов

Теперь  цвета задаются как CSS-переменные, которые можно менять динамически.

```scss
// src/assets/scss/base/_variables.scss

// === Breakpoints ===
$vp-xs: 375px;
$vp-sm: 576px;
$vp-md: 768px;
$vp-lg: 992px;
$vp-xl: 1200px;
$vp-xxl: 1400px;

// === Цвета для тем ===
:root {
  // Тёмная тема (по умолчанию)
  --color-bg: #2f4454;
  --color-text: #f0f8ff;
  --color-primary: #2e151b;
  --color-secondary: #da7b93;
  --color-accent: #376e6f;
  --color-border: #ccc;
}

[data-theme="light"] {
  // Светлая тема
  --color-bg: #f8f9fa;
  --color-text: #212529;
  --color-primary: #495057;
  --color-secondary: #007bff;
  --color-accent: #20c997;
  --color-border: #dee2e6;
}
```

### Обновление `_global.scss`

```scss

// src/assets/scss/global/_global.scss

html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
}

a {
  color: inherit;
  text-decoration: none;
  outline: none;
}

body {
  background-color: var(--color-bg);
  color: var(--color-text);
  font-family: "Montserrat", sans-serif;
  margin: 0;
  transition: background-color 0.3s ease; 
}

```

### Добавление кнопки для смены темы и логики в `Header.vue`

```vue
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


```

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
