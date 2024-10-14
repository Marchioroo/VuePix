<template>


  <div class="container mx-auto p-4 cursor-pointer " >
    <div class="w-full h-0.5 w-full  bg-gray-200 justify-start w-full max- md:w-1/3 lg:w-[30%]" ></div>
    <div class=" mt-3 flex items-center justify-start w-full md:w-1/3 lg:w-[30%]" >
    <img src="../src/assets/ic/ic-pix.svg" class="mr-2 w-6 h-6">
  
    <button @click="openModal" class=" text-black rounded w-full flex flex-row justify-start"> Pix e saques </button>

    <img src="../src/assets/ic/ic-Arrows-Tipe_2-Direction_Right.svg" class="mr-2 ml-auto w-6 h-4">
    <ModalPage :isOpen="isModalOpen" @close="closeModal" />
  </div>
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
     
      this.isModalOpen = true;
    },
    closeModal() {
    
      this.isModalOpen = false; 
    },
  },
};
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Manrope:wght@200..800&display=swap'),
</style>
