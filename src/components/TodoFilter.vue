<template>
    <div class="filter">
      <label>
        <input type="checkbox" :checked="filterCompleted" @change="$emit('toggleFilter')" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>
  </template>
  
  <script setup>
  defineProps(['filterCompleted'])
  </script>
  
  <style scoped>
  .filter {
    margin-bottom: 1rem;
    font-weight: bold;
    color: #34495e;
  }
  </style>
  