<template>
  <div class="modal" v-if="isOpen">
    <div class="modal-content w-full h-full md:h-2/3 xl:h-full md:w-2/3 bg-white rounded shadow flex flex-col p-4">
      
      <div class="icVoltar flex flex-row w-full p-3 mt-2">
        <img src="../assets/ic/ic-Arrows-Tipe_1-Direction_Left.svg" class="size-6" @click="closeModal" alt="">
        <h2 class="ml-2">Pix e saques</h2>
      </div>
      <hr class=" w-full">

      <p class="text-4xl md:text-xl lg:text-2xl  mt-11 font-semibold">Adicionar chave pix</p>
      <p class="pt-2 mb-3  text-gray-600">Preencha os dados abaixo.</p>

      <form @submit.prevent="handleSubmit" class="mt-5 flex-grow flex flex-col">
        <div class="mb-4 flex flex-col">
          <label for="nome">Nome completo</label>
          <input class="" minlength="7" type="text" id="nome" v-model="formData.nome"
            placeholder="Digite o seu nome completo..." />
        </div>
        <div class="mb-4 flex flex-col">
          <label for="email">Chave pix</label>
          <input type="text" minlength="7" id="email" v-model="formData.email"
            placeholder="Digite a sua chave pix..." />
        </div>
        <div class="mb-4 flex flex-col">
          <label for="telefone">Apelido</label>
          <input type="tel" minlength="4" id="telefone" v-model="formData.telefone"
            placeholder="Digite um apelido para a chave pix..." />
        </div>

        <!-- O botão agora ficará na parte inferior -->
        <div class="flex items-center justify-center mt-auto">
          <button type="submit" class="font-semibold w-full max-w-[335px] bg-[#CCCCCC] text-[#4A4A4A] hover:bg-[#0F0A14] hover:text-[white] transition-all p-2 mb-9 rounded-3xl flex justify-center">
           Adicionar chave
          </button>
        </div>
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
      errors: {},
    };
  },
  methods: {
    closeModal() {
      console.log('Modal fechado');
      this.$emit('close'); // Emite um evento para o componente pai
    },
    handleSubmit() {
      console.log('Formulário enviado:', this.formData);

      // Limpa mensagens de erro anteriores
      this.errors = {};

      // Validação de campos
      if (!this.formData.nome) {
        this.errors.nome = 'Nome é obrigatório.';
        console.log('Erro: Nome é obrigatório.');
      }
      if (!this.formData.email) {
        this.errors.email = 'Chave PIX é obrigatória.';
        console.log('Erro: Chave PIX é obrigatória.');
      } else {
        // Validação da Chave PIX
        if (!this.validarChavePix(this.formData.email)) {
          this.errors.email = 'Chave PIX inválida. Deve ser um telefone, email ou chave Pix.';
          console.log('Erro: Chave PIX inválida.');
        }
      }
      if (!this.formData.telefone) {
        this.errors.telefone = 'Apelido é obrigatório.';
        console.log('Erro: Apelido é obrigatório.');
      }

      // Verifica se existem erros
      if (Object.keys(this.errors).length > 0) {
        console.log('Por favor, preencha todos os campos corretamente!');
        alert('Erro: Por favor, preencha todos os campos corretamente!');
        return; // Não fecha o modal se houver erros
      }

      // Se todos os campos estiverem preenchidos e válidos, fecha o modal
      this.closeModal();
      alert('Dados enviados com sucesso!'); // Mensagem de sucesso
    },
    validarChavePix(chave) {
      const telefoneRegex = /^\(\d{2}\) \d{5}-\d{4}$/; // Exemplo: (11) 91234-5678
      const emailRegex = /^\S+@\S+\.\S+$/; // Exemplo: exemplo@dominio.com
      const pixRegex = /^[a-zA-Z0-9]{1,50}$/; // Exemplo: chavePix1234

      return telefoneRegex.test(chave) || emailRegex.test(chave) || pixRegex.test(chave);
    },
    formatarTelefone(event) {
      let input = event.target.value.replace(/\D/g, ''); // Remove todos os caracteres não numéricos
      if (input.length > 2) {
        input = `(${input.slice(0, 2)}) ${input.slice(2)}`; // Adiciona parênteses
      }
      if (input.length > 9) {
        input = `${input.slice(0, 9)}-${input.slice(9)}`; // Adiciona traço
      }
      this.formData.telefone = input; // Atualiza o valor formatado no data
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
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@200..800&display=swap');

* {
  font-family: 'Manrope';
}

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);

}



.icVoltar {
  width: 100%;

}

.button {}

hr {
  background-color: #E6E6E6;
}

.modal-content {
  background-color: white;
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);

}


input {
  outline: none;
  border-bottom: 1px solid #979696;
  padding: 7px 0px 7px 0px;

}
</style>
