<template>
    <div class="app">
        <h1>ToDos</h1>
        <input type="text" v-model="todoName" @keyup.enter="addTodo">
        <ul>
            <li v-for="todo in todos" :key="todo.id" style="list-style: none;">
                {{todo.name}}
            </li>
        </ul>
    </div>
</template>

<script>
const baseURL = "http://localhost:3000/todos"
import axios from 'axios'
export default {
    data() {
        return{
            todos: [],
            todoName: ''
        }
    },

    async created() {
        try {
            const res = await axios.get(baseURL)
            this.todos = res.data
        }
        catch(e) {
            console.error(e);
        }
    },

    methods: {
        async addTodo() {
            const res = await axios.post(baseURL, {name: this.todoName})
            this.todos = [...this.todos, res.data]
            this.todoName = ''
        }
    }
}
</script>

<style scoped>
.app {
    text-align: center;
}
</style> 






