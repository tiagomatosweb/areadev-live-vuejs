<template>
    <div>
        <div class="text-white">
            {{ fullName }}
        </div>

        <section class="grid grid-cols-2 gap-4">
            <div class="bg-teal-700 rounded-lg p-2">
                Todos done
                <div class="text-lg">
                    {{ todosDone }}
                </div>
            </div>

            <div class="bg-teal-700 rounded-lg p-2">
                Todos undone
                <div class="text-lg">
                    {{ todosUnDone }}
                </div>
            </div>
        </section>

        <section class="space-x-2 mt-5">
            <input
                v-model="newTodo"
                type="text"
                class="text-white bg-gray-700 p-2 rounded"
                @keyup.enter="addTodo()"
            >
            <button
                @click="addTodo()"
                class="bg-green-400 p-2 rounded">Adicionar</button>
        </section>

        <section class="bg-gray-800 mt-5">
            <div class="space-y-2">
                <Todo
                    v-for="todo in todos"
                    :todo="todo"
                    @onClick="toggleTodo"
                    @onRemove="removeTodo"
                />
            </div>
        </section>
    </div>
</template>

<script>
import CheckIcon from './components/CheckIcon.vue'
import Todo from './components/Todo.vue'

// Options API
export default {
    components: {
        CheckIcon,
        Todo
    },

    data() {
        return {
            newTodo: '',
            todos: [],
            firstName: 'Bruno',
            lastName: 'Lima'
        }
    },

    beforeCreate() {},
    created() {
       this.getTodos()
    },

    beforeMount() {},
    mounted() {},

    beforeUnmount() {},
    unmounted() {},

    watch: {},

    computed: {
        fullName() {
            return `${this.firstName} ${this.lastName}`
        },
        todosDone() {
            return this.todos.filter(o => o.is_done).length
        },
        todosUnDone() {
            return this.todos.filter(o => !o.is_done).length
        },
    },

    methods: {
        getTodos() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
                .then(response => response.json())
                .then(json => {
                    this.todos = json
                })
        },
        addTodo() {
            this.todos.push({
                title: this.newTodo,
                is_done: false
            })

            this.newTodo = ''
        },
        toggleTodo(todo) {
            todo.is_done = !todo.is_done
        },
        removeTodo(todo) {
            const idx = this.todos.findIndex(o => o.title === todo.title)
            this.todos.splice(idx, 1)
        }
    }
}
</script>
