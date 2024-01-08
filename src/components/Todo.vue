<!-- Todo.vue -->

<template>
  <div class="p-4 mx-auto max-w-xl">
    <div class="flex flex-col gap-4">
    <h1 class="text-2xl font-bold">Todos</h1>

    <TodoInput @add-todo="addTodo"/>
    
    <TodoList 
      :todos="todos"
      @remove-todo="removeTodo" 
    />
  </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import TodoInput from './TodoInput.vue';
import TodoList from './TodoList.vue';

export interface Todo {
  id: string
  text: string
  done: boolean
}

// State todos
const todos = ref<Todo[]>([])

// Load todos
const savedTodos = localStorage.getItem('todos')
if (savedTodos) {
  todos.value = JSON.parse(savedTodos)
}

// Thêm todo
function addTodo(text: string) {
  const newTodo: Todo = {
    id: new Date().toISOString(),
    text,
    done: false
  }

  todos.value.push(newTodo)
  saveToLocalStorage()
}

// Xóa todo
function removeTodo(todo: Todo) {
  todos.value = todos.value.filter(t => t.id !== todo.id)
  saveToLocalStorage()
}

// Lưu vào localStorage
function saveToLocalStorage() {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}
</script>