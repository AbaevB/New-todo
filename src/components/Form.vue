<!-- src/components/Form.vue -->
<script setup>
import { ref } from 'vue';
import Btn from './Btn.vue';
const btnContent = 'Add';

const inputValue = ref('');
const emit = defineEmits('submit');

const handleSubmit = () => {
    if (inputValue.value.trim()) {
        emit('submit', inputValue.value)
        inputValue.value = '';
    }
}

</script>
<template>
    <form  class="form">
        <input
        v-model="inputValue"
        type="text"
        placeholder="New todo"
        class="form__field"
        aria-label="New todo"
        >
        <Btn 
        :content="btnContent"
          btn-class="form__btn"
          btn-type="submit"
          btn-aria-label="Add new todo"
          @click="handleSubmit"
        />
    </form>
</template>