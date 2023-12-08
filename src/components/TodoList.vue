<script>
export default {
  props: {
    todos: Array,
  },

  methods: {
    editTodo(todo) {
      // Toggle the edit mode on the todo object
      todo.editing = !todo.editing;

      // IF entering the edit mode, save the current content for later comparison

      if (todo.editing) {
        todo.originalContent = todo.content;
      } else {
        // If exiting the edit mode, check if the content has changed
        if (todo.content.trim() === "") {
          // If the content is empty, revert to the original content
          todo.content = todo.originalContent;
        }
        // Remove the original content property
        delete todo.originalContent;
      }
    },

    removeTodo(todo) {
      // Remove the todo object from the todos array

      const index = this.todos.indexOf(todo);
      if (index !== -1) {
        this.todos.splice(index, 1);
      }
    },
  },
};
</script>

<template>
  <section class="todo-list">
    <h4>YOUR TODO LIST</h4>

    <ul class="todos">
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{ completed: todo.completed }">
            <!-- Conditionally render either input or span based on editing state-->
            <template v-if="todo.editing">
                <input v-model="todo.content" @blur="editTodo(todo)" @keydown.enter="editTodo(todo)" />
            </template>
            <template v-else>
                {{ todo.content }}
            </template>
        </span>
        <button @click="editTodo(todo)">✍</button>
        <button @click="removeTodo(todo)">🗑️</button>
      </li>
    </ul>
  </section>
</template>

<style scoped>

.todo-list {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  align-items: center;
}

.todos {
  list-style: none;
  padding: 0;
}

.todos li {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
  color: #646cff;
}

.todos li input[type="checkbox"] {
  margin-right: 1rem;
}

.completed {
  text-decoration: line-through;
}

.todos button {
  font-size: 1em;
  margin-left: 1.5rem;
  cursor: pointer;
}

.todos li button:hover {
  color: #ff0000;
}

.todos li::marker {
  content: "📌";
  color: #ff0000;
}

h4 {
  font-size: 2em;
  margin-bottom: 1rem;
  color: #646cff;
}

input:not([type="radio"]):not([type="checkbox"]),
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
