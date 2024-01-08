<template>
  <ul class="flex flex-col gap-2">
    <li
      v-for="todo in todos"
      :key="todo.id"
      class="flex justify-between p-2 border" 
    >
      <span>{{ todo.text }}</span>
      <button @click="removeTodo(todo)">
        X
      </button>
    </li>
  </ul>
</template>

<script lang="ts">
import { toRefs } from 'vue'
import type { Todo } from './Todo.vue'

export default {
  props: {
    todos: {
      type: Array as () => Todo[],
      required: true
    }
  },

  setup(props, { emit }) {

    const { todos } = toRefs<{ todos: Todo[] }>(props)

    function removeTodo(todo: Todo) {
      emit('remove-todo', todo)
    }

    return {
      todos,
      removeTodo
    }
  }
}  
</script>