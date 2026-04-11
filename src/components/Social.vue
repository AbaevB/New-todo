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