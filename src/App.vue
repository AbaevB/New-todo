<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import Footer from './components/Footer.vue';
</script>

<template>
 <Header />

  <main class="main">
    
    <div class="container">
      <Form />  
    </div>
    
  </main>
  <Footer />
</template>


