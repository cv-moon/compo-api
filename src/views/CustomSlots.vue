<template>
  <h1>Aprendiendo Slots</h1>
  <button>Abrir Modal</button>
  <modal v-if="isOpen" title="Hola Mundo" @on:close="closeModal">
    <!-- <button>Salir</button>
        <p>
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Recusandae
          laborum officiis a!
        </p>
    <h1>Título del Modal</h1> -->
    <template v-slot:footer>
      <button @click="closeModal">Salir</button>
    </template>
    <template v-slot:header>
      <h2>Título del Modal</h2>
    </template>
    <template v-slot:body>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Recusandae
        laborum officiis a!
      </p>
    </template>
  </modal>
</template>

<script>
import { ref } from "vue";
import Modal from "../components/Modal.vue";
export default {
  components: { Modal },
  setup() {
    const isOpen = ref(false);
    return {
      isOpen,

      openModal: () => (isOpen.value = true),
      closeModal: () => (isOpen.value = false),
    };
  },
};
</script>

<style scoped>
</style>