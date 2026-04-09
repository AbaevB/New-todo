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
