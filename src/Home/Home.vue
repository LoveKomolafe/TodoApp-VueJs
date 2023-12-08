<script>
import { ref } from "vue";
import AddTodo from "../components/AddTodo.vue";
import TodoList from "../components/TodoList.vue";

export default {
  components: {
    AddTodo,
    TodoList,
  },

  setup() {
    const name = ref("");
    const todos = ref([]);

    return {
      name,
      todos,
    };
  },
};
</script>

<template>
  <main class="todoApp">
    <section class="greetings">
      <input type="text" placeholder="Name here" v-model="name" />

      <h1 class="title">
        <span>👋</span> Hello {{ name }},
        Welcome to your todo task!
      </h1>
    </section>

    <AddTodo :todos="todos" />
    <TodoList :todos="todos" />
  </main>
</template>

<style scoped>

.todoApp {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

.greetings .title {
  display: flex;
}

.greetings .title input {
  flex: 1 1 0%;
  min-width: 0;
}

.greetings .title,
.greetings input, .title {
  color: var (--color-primary);
  font-size: 3.2em;
  font-weight: 700;
}

input:not([type="radio"]):not([ype="checkbox"]),
button {
  appearance: none;
  border: none;
  outline: none;
  background: none;
  cursor: initial;
  font-size: 1.5em;
  font-weight: bolder;
  color: #646cff;
  margin: 0;
  padding: 0;
}
</style>
