<template>
    <div class="todo-list">
      <h2>To-Do List</h2>
      
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" placeholder="Add a new to-do" />
        <button type="submit">Add</button>
      </form>
  
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  // Reactive references for newTodo and todos
  const newTodo = ref('');
  const todos = ref([]);
  
  // Function to add a new to-do item
  const addTodo = () => {
    if (newTodo.value.trim()) {
      todos.value.push({ text: newTodo.value, done: false });
      newTodo.value = ''; // Clear the input after adding
    }
  };
  
  // Function to remove a to-do item
  const removeTodo = (index) => {
    todos.value.splice(index, 1);
  };
  </script>
  
  <style scoped>
  .todo-list {
    max-width: 400px;
    margin: 0 auto;
  }
  
  input[type="checkbox"] {
    margin-right: 10px;
  }
  
  .done {
    text-decoration: line-through;
    color: #999;
  }
  
  form {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  button {
    margin-left: 10px;
    padding: 5px 10px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  </style>
  