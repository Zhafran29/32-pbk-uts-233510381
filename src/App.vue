<template>
  <div class="wrapper">
    <div class="container">
      <h1>🚀 SpaceMan</h1>

      <form @submit.prevent="addTodo" class="input-group">
        <input v-model="newTodo" placeholder="Apa yang ingin kamu lakukan hari ini?" />
        <button type="submit">Tambah</button>
      </form>

      <div class="filter-options">
        <label><input type="radio" value="all" v-model="filterOption" /> Semua</label>
        <label><input type="radio" value="pending" v-model="filterOption" /> Belum Selesai</label>
        <label><input type="radio" value="completed" v-model="filterOption" /> Sudah Selesai</label>
      </div>

      <ul class="todo-list">
        <TodoItem
          v-for="todo in filteredTodos"
          :key="todo.id"
          :todo="todo"
          @toggle="toggleTodo"
          @cancel="cancelTodo"
        />
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TodoItem from './components/TodoItem.vue'

const todos = ref([])
const newTodo = ref('')
const filterOption = ref('all')

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value.trim(),
      completed: false,
      canceled: false,
    })
    newTodo.value = ''
  }
}

const toggleTodo = (id) => {
  const todo = todos.value.find(t => t.id === id)
  if (todo) todo.completed = !todo.completed
}

const cancelTodo = (id) => {
  const todo = todos.value.find(t => t.id === id)
  if (todo) todo.canceled = true
}

const filteredTodos = computed(() => {
  if (filterOption.value === 'pending') {
    return todos.value.filter(todo => !todo.completed && !todo.canceled)
  } else if (filterOption.value === 'completed') {
    return todos.value.filter(todo => todo.completed && !todo.canceled)
  } else {
    return todos.value.filter(todo => !todo.canceled)
  }
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600&display=swap');

.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #1f1f2e;
  padding: 1rem;
  color: #ffffff;
  font-family: 'Orbitron', sans-serif;
}

.container {
  background: #2c2c3e;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 0 25px rgba(0, 255, 255, 0.1);
  width: 100%;
  max-width: 600px;
}

h1 {
  text-align: center;
  font-size: 2rem;
  color: #8be9fd;
  margin-bottom: 2rem;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 1rem;
}

input[type="text"] {
  flex: 1;
  padding: 0.7rem 1rem;
  border-radius: 8px;
  border: none;
  background: #3d3d5c;
  color: #fff;
  font-size: 1rem;
  outline: none;
}

button {
  background: #8be9fd;
  border: none;
  color: #1f1f2e;
  font-weight: bold;
  padding: 0.7rem 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 0 10px #8be9fd80;
  transition: 0.3s ease;
}
button:hover {
  background: #50fa7b;
  box-shadow: 0 0 15px #50fa7b80;
}

.filter-options {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin: 1rem 0;
  color: #bd93f9;
  font-weight: bold;
  font-size: 0.95rem;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin-top: 1rem;
}
</style>
