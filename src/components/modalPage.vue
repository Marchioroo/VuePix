<template>
  <div class="modal" v-if="isOpen">
    <div class="modal-content w-full h-full m-2">

      
      <div class="icVoltar flex flex-row w-ful p-3 mt-2">
        <img src="../assets/ic/ic-Arrows-Tipe_1-Direction_Left.svg" class="size-6" @click="closeModal" alt="">
        <h2 class="ml-2">Pix e saques</h2>
     
      </div>
      <hr>
     
      <p class="text-4xl md:text-xl lg:text-2xl p-1 ml-1 mt-9">Adicionar chave pix</p>
      <p class="p-1 ml-1 text-gray-600">Preencha os dados abaixo.</p>

      <form @submit.prevent="handleSubmit" class="mt-6 p-2">
        <div class="mb-4 flex flex-col">
          <label for="nome">Nome Completo</label>
          <input class="" type="text" id="nome" v-model="formData.nome" placeholder="Digite o seu nome completo..." />
        </div>
        <div class="mb-4 flex flex-col">
          <label for="email">Chave pix</label>
          <input type="email" id="email" v-model="formData.email" placeholder="Digite a sua chave pix..." />
        </div>
        <div class="mb-4 flex flex-col">
          <label for="telefone">Apelido</label>
          <input type="tel" id="telefone" v-model="formData.telefone" placeholder="Digite um apelido para a chave pix..." />
        </div>
        <button type="submit">Adicionar chave</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalPage',
  props: {
    isOpen: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      formData: {
        nome: '',
        email: '',
        telefone: '',
      },
    };
  },
  methods: {
    closeModal() {
      console.log('Modal fechado');
      this.$emit('close');
    },
    handleSubmit() {
      console.log('Formulário enviado:', this.formData);
      // Aqui entra a lógica de validação...
    },
  },
  watch: {
    isOpen(newVal) {
      console.log('Estado do modal mudou:', newVal);
    },
  },
};
</script>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
 
}
.icVoltar{
  width: 100%;
  
}

.modal-content {
  background-color: white;
 
  border-radius: 5px;
  width: 100%;
  height: 100%; 
 
}

.close {
  cursor: pointer;
  float: right;
  font-size: 20px;
}
input{
  gap:0;
  padding:10px;
}
</style>
