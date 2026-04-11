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

## Футер

Создан компонент `Footer.vue` 

### Иконки

Созданы Vue-иконки социальных сетей. Пример:

```vue
<!-- src/components/icons/IconVK.vue -->
<script setup>
defineProps({
  size: { type: String, default: '24px' },
  color: { type: String, default: '#fff' }
})
</script>

<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :width="size"
    :height="size"
    viewBox="0 0 24 24"
    role="img"
    aria-label="Логотип ВКонтакте"
    aria-hidden="true"
    
  >
     <path d="m9.489.004.729-.003h3.564l.73.003.914.01.433.007.418.011.403.014.388.016.374.021.36.025.345.03.333.033c1.74.196 2.933.616 3.833 1.516.9.9 1.32 2.092 1.516 3.833l.034.333.029.346.025.36.02.373.025.588.012.41.013.644.009.915.004.98-.001 3.313-.003.73-.01.914-.007.433-.011.418-.014.403-.016.388-.021.374-.025.36-.03.345-.033.333c-.196 1.74-.616 2.933-1.516 3.833-.9.9-2.092 1.32-3.833 1.516l-.333.034-.346.029-.36.025-.373.02-.588.025-.41.012-.644.013-.915.009-.98.004-3.313-.001-.73-.003-.914-.01-.433-.007-.418-.011-.403-.014-.388-.016-.374-.021-.36-.025-.345-.03-.333-.033c-1.74-.196-2.933-.616-3.833-1.516-.9-.9-1.32-2.092-1.516-3.833l-.034-.333-.029-.346-.025-.36-.02-.373-.025-.588-.012-.41-.013-.644-.009-.915-.004-.98.001-3.313.003-.73.01-.914.007-.433.011-.418.014-.403.016-.388.021-.374.025-.36.03-.345.033-.333c.196-1.74.616-2.933 1.516-3.833.9-.9 2.092-1.32 3.833-1.516l.333-.034.346-.029.36-.025.373-.02.588-.025.41-.012.644-.013.915-.009ZM6.79 7.3H4.05c.13 6.24 3.25 9.99 8.72 9.99h.31v-3.57c2.01.2 3.53 1.67 4.14 3.57h2.84c-.78-2.84-2.83-4.41-4.11-5.01 1.28-.74 3.08-2.54 3.51-4.98h-2.58c-.56 1.98-2.22 3.78-3.8 3.95V7.3H10.5v6.92c-1.6-.4-3.62-2.34-3.71-6.92Z" :fill="color"/> 
      
  </svg>
</template>

```

### Блок соцсетей

Создан и подключен в футер элемент `Social.vue` со ссылками на соцсети:

```vue
<!-- src/components/Social.vue -->
<script setup>
import IconVK from './icons/IconVK.vue';
import IconX from './icons/IconX.vue';
import IconTg from './icons/IconTg.vue';
import IconLinkedin from './icons/IconLinkedin.vue';
import IconGithub from './icons/IconGithub.vue';
import IconBluesky from './icons/IconBluesky.vue';

// Цвет иконок — можно менять под тему
const iconColor = 'var(--color-text)';
</script>
<template>
    <ul class="social">
    <li class="social__item">
      <a
        href="https://vk.com/andrewbaev"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Моя страница ВКонтакте (открывается в новой вкладке)"
      >
        <IconVK :color="iconColor" size="24" />
      </a>
    </li>
    <li class="social__item">
      <a
        href="https://x.com/AbaevB70"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Профиль на X (бывший Twitter) (открывается в новой вкладке)"
      >
        <IconX :color="iconColor" size="24" />
      </a>
    </li>
    <li class="social__item">
      <a
        href="https://web.telegram.org/"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Telegram (открывается в новой вкладке)"
      >
        <IconTg :color="iconColor" size="24" />
      </a>
    </li>
    <li class="social__item">
      <a
        href="https://www.linkedin.com/in/andrewbaev1970/"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Профиль на LinkedIn (открывается в новой вкладке)"
      >
        <IconLinkedin :color="iconColor" size="24" />
      </a>
    </li>
    <li class="social__item">
      <a
        href="https://github.com/AbaevB"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Репозиторий на GitHub (открывается в новой вкладке)"
      >
        <IconGithub :color="iconColor" size="24" />
      </a>
    </li>
    <li class="social__item">
      <a
        href="https://bsky.app/profile/abaevb.bsky.social"
        target="_blank"
        rel="noopener"
        class="social__link"
        aria-label="Профиль на Bluesky (открывается в новой вкладке)"
      >
        <IconBluesky :color="iconColor" size="24" />
      </a>
    </li>
  </ul>
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
