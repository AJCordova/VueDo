
<template>
    <div class = "wrapper">
        <h1>A TODO List</h1>
        <form @submit.prevent = ""> 
            <input type= "text" name="todo-text"  v-model="newTodoText" placeholder="Create a new todo item here!">
        </form>
        <ul v-if="todos.length">

        </ul>
        <p class="none" v-else> Nothing here yet. Let's add a new task!</p>
    </div>
</template>

<script>
import TaskItem from "/TaskItem.vue"

let nextTodoId = 1

function createTodo(text) {
return ({
text,
id: nextTodoId++
})
}

export default { 
    components: {
        TaskItem
    },

    data() {
        return {
            todos: [], 
            newTodoText: ""
        }
    },

    methods: {
        addTodo() {
            const trimmedText = this.newTodoText.trim()

            if (trimmedText) {
                this.todos.push(createTodo(trimmedText))
            }

            this.newTodoText = ""
        },

        removeTodo(item) {
            this.todos = this.todos.filter(todo => todo !== item)
        }
    }
}
</script>

<style scoped>
*, *::before, *::after {
    box-sizing: border-box
}

html, body {
    font: 16px / 1.2 BlinkMacSystemFont, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif
    padding 10px
}

.wrapper {
    width: 100%
    margin 0 auto
}

form {
    margin-bottom: 20px
}


input[type="text"] {
    width: 100%
    padding 10px
    border 1px solid #1e1717
}

ul, li {
    margin: 0
    padding 0 
}

p.none {
    color: #184723
    font-size small
}
</style>