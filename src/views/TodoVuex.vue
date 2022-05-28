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
</template>
<script>
import useTodos from "../composables/useTodos";
export default {
  setup() {
    const { pending, currentTab, getTodosByTab, toggleTodo } = useTodos();

    return {
      pending,
      currentTab,
      getTodosByTab,
      toggleTodo,
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