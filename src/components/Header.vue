<!-- src/components/Header.vue -->

<script setup>
import Btn from './Btn.vue';
function changeTheme(){
    console.log('Change Theme');
}




</script>
<template>
    <header class="header">
        <div class="container">
            <div class="header__content">
                <img src="/images/logo.png" alt="TODO logo"> 
                <h1 class="header__title">TODO List</h1>
                <Btn
                content = 'Сменить тему'
                btn-class="header__btn"
                btn-type="button"
                @click="changeTheme"
                />

                
            </div>

        </div>

    </header>
</template>