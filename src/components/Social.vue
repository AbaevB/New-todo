<!-- src/components/Social.vue -->
<script setup>
import IconVK from './icons/IconVK.vue';
import IconX from './icons/IconX.vue';
import IconTg from './icons/IconTg.vue';
import IconLinkedin from './icons/IconLinkedin.vue';
import IconGithub from './icons/IconGithub.vue';
import IconBluesky from './icons/IconBluesky.vue';
</script>
<template>
    <ul class="social">
        <li class="social__item">
            <a href="https://vk.com/andrewbaev" class="social__link">
               <IconVK />
            </a>
        </li>
        <li class="social__item">
            <a href="https://x.com/AbaevB70" class="social__link">
                <IconX />
            </a>
        </li>

        <li class="social__item">
            <a href="https://web.telegram.org/" class="social__link">
                <IconTg />
            </a>
        </li>
        <li class="social__item">
            <a href="https://www.linkedin.com/in/andrewbaev1970/" class="social__link">
                <IconLinkedin />
            </a>
        </li>

        <li class="social__item">
            <a href="https://github.com/AbaevB" class="social__link">
                <IconGithub />
            </a>
        </li>
        <li class="social__item">
            <a href="https://bsky.app/profile/abaevb.bsky.social" class="social__link">
                <IconBluesky />
            </a>
        </li>
    </ul>
</template>