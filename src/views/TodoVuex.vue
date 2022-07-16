<template>
  <h1>Lista de tareas de Thanos</h1>
  <!-- <h4>{{ $store.state.todos.length }}</h4> -->
  <h4>Pendientes: {{ pending.length }}</h4>
  <hr />

  <button @click="currentTab = 'all'" :class="{ active: currentTab === 'all' }">
    Todos
  </button>
  <button
    @click="currentTab = 'pending'"
    :class="{ active: currentTab === 'pending' }"
  >
    Pendientes
  </button>
  <button
    @click="currentTab = 'completed'"
    :class="{ active: currentTab === 'completed' }"
  >
    Completados
  </button>

  <div>
    <ul>
      <li
        v-for="todo in getTodosByTab"
        :key="todo.id"
        :class="{ completed: todo.completed }"
        @dblclick="toggleTodo(todo.id)"
      >
        {{ todo.text }}
      </li>
    </ul>
  </div>
  <button @click="isOpen = true">Crear Todo</button>

  <!--Modal-->
  <modal v-if="isOpen" @on:close="isOpen = false">
    <template v-slot:header>
      <h1>Nueva Tarea</h1>
    </template>
    <template v-slot:body>
      <form>
        <input type="text" placeholder="Nueva Tarea" />
      </form>
      <br />
      <br />
      <button type="submit">Crear</button>
    </template>
  </modal>
</template>
<script>
import useTodos from "../composables/useTodos";
import Modal from "../components/Modal";
import { ref } from "vue";
export default {
  components: { Modal },
  setup() {
    const { pending, currentTab, getTodosByTab, toggleTodo } = useTodos();

    return {
      pending,
      currentTab,
      getTodosByTab,
      toggleTodo,
      isOpen: ref(false),
    };
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: center;
  text-align: center;
}
ul {
  width: 300px;
  text-align: left;
}
li {
  cursor: pointer;
}
.active {
  background-color: #2c3e50;
  color: white;
}
.completed {
  text-decoration: line-through;
}
</style>