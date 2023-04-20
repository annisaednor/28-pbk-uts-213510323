<script>
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Makan Bergizi', done: true },
        { id: id++, text: 'Makan Berprotein', done: true },
        { id: id++, text: 'Olahraga 3x1 minggu', done: false }
      ]
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>

<template>
    <div class="container">
        <div class="konten">
    <h1>Rutinitas Hidup Sehat</h1>
  <form @submit.prevent="addTodo">
    <input class="input" v-model="newTodo" >
    <button>Add</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
        <div class="list">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </div>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
    </div>
  </div>
</template>


<style>
.done {
  text-decoration: line-through;
}
button{
    color: black;
}
</style>