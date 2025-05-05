<template>
    <li :class="['todo-item', { completed: todo.completed, canceled: todo.canceled }]">
      <input
        type="checkbox"
        :checked="todo.completed"
        @change="$emit('toggle', todo.id)"
        :disabled="todo.canceled"
      />
      <span>{{ todo.text }}</span>
      <button @click="$emit('cancel', todo.id)" :disabled="todo.canceled">Batal</button>
    </li>
  </template>
  
  <script setup>
  defineProps(['todo'])
  </script>
  
  <style scoped>
  .todo-item {
    display: flex;
    align-items: center;
    gap: 10px;
    background: #3a3a55;
    padding: 0.8rem 1rem;
    border-radius: 10px;
    margin-bottom: 12px;
    color: #f8f8f2;
    box-shadow: 0 2px 6px rgba(0, 255, 255, 0.1);
  }
  
  .todo-item.completed span {
    text-decoration: line-through;
    color: #8be9fd;
  }
  
  .todo-item.canceled span {
    text-decoration: line-through;
    color: #ff5555;
  }
  
  input[type="checkbox"] {
    accent-color: #8be9fd;
  }
  
  button {
    margin-left: auto;
    background: #ff5555;
    border: none;
    color: white;
    padding: 0.4rem 0.8rem;
    border-radius: 6px;
    cursor: pointer;
    transition: 0.3s ease;
  }
  button:hover {
    background: #ff6e6e;
  }
  </style>
  