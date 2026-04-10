<!-- src/components/Btn.vue -->
 <script setup>
 defineProps({
     content: {
        type: String,
        required: true,
     },
     btnClass: {
        type: [String, Array],
        default: '',
     },
     btnType: {
        type:String,
     },
     btnAriaLabel:{
        type: String,
     }
 })

 // Передаём все события наверх (например, @click)
defineEmits(['click'])

</script>
<template>
    <button
    class="btn"
    :class="btnClass"
    :type="btnType"
    :aria-label="btnAriaLabel"
    @click="$emit('click')"
    >
       {{ content }} 
    </button>
</template>