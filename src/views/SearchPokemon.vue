<template>
  <h1>Buscar pokemon: {{ pokemonId }}</h1>
  <form @submit.prevent="onSubmit">
    <input
      type="number"
      placeholder="Número de pokemon"
      autofocus
      v-model="pokemonId"
      ref="txtSearchId"
    />
    <br />
    <span>Presione enter para buscar</span>
  </form>
</template>

<script>
import { ref, onActivated } from "vue";
import { useRouter } from "vue-router";
export default {
  setup() {
    const router = useRouter();

    const pokemonId = ref(1);

    const txtSearchId = ref();

    onActivated(() => {
      // txtSearchId.value.focus()
      txtSearchId.value.select();
    });

    return {
      pokemonId,
      txtSearchId,
      onSubmit: () => {
        router.push({ name: "pokemon-id", params: { id: pokemonId.value } });
      },
    };
  },
};
</script>

<style>
</style>