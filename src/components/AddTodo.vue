<script>
import { ref, onMounted, computed, watch } from 'vue'

export default {
    name: 'AddTodo',

    props: {
        todos: Array,
    },

    setup(props) {

        const input_todo = ref('')

        const todos_count = computed(() => todos.value.sort((a, b) => {
        return a.createdAt - b.createdAt
        }))

        onMounted(() => {
            console.log('Component is mounted!')
        })

        watch(input_todo, (newValue, oldValue) => {
            console.log('input_todo changed from', oldValue, 'to', newValue)
        })

        const addTodo = () => {
            if (input_todo.value === '') {
                return
            }

            props.todos.push({
                content: input_todo.value,
                completed: false,
                createdAt: new Date().getTime() 
            })
            
            // Clearing the input field after adding a todo
            input_todo.value = ''
        };

        return {
            input_todo,
            todos_count,
            addTodo
        }
    },
}

</script>

<template>
    <section class="create-todo">

        <form class="todo-form" @submit.prevent="addTodo" id="form">
            <h3>What's on your Todo List?</h3>
            <input 
                type="text" 
                placeholder="Add your todo task here" v-model="input_todo" 
            /> 
            
            <button type="submit" @keydown.enter="addTodo">➕</button>
        </form>
    </section>
</template>

<style scoped>

.create-todo {
    width: 200%;
    max-width: 500px;
    margin: 0 auto;
    align-items: center;
}

.todo-form h3 {
    font-size: 1.5em;
    margin-bottom: 1rem;
    color: #646cff;
}

.todo-form input {
    width: 100%;
    padding: 0.5rem;
    font-size: 1.2em;
    border: 1px solid #646cff;
    border-radius: 0.5rem;
    margin-bottom: 1rem;
    transition: border-radius 0.3s, box-shadow 0.3s;
}

.todo-form button {
    font-size: 1.2em;
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    background-color: #646cff;
    color: #fff;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s;
}

.todo-form button:hover {
    background-color: #fff;
    color: #646cff;
    border: 1px solid #646cff;
}

</style>