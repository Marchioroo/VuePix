<template>
  <div class="container mx-auto p-4 ">
    
    <button @click="openModal" class="mt-4 bg-green-500 text-white p-2 rounded">Pix e saques</button>
    <ModalPage :isOpen="isModalOpen" @close="closeModal" />
  </div>
</template>

<script>
import ModalPage from './components/modalPage.vue';

export default {
  name: 'App',
  components: {
    ModalPage,
  },
  data() {
    return {
      isModalOpen: false, 
    };
  },
  methods: {
    openModal() {
      console.log('Abrindo o modal...');
      this.isModalOpen = true;
    },
    closeModal() {
      console.log('Fechando o modal...');
      this.isModalOpen = false; 
    },
  },
};
</script>

<style>
</style>
