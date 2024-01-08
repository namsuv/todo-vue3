<template>
  <form @submit="onSubmit">
    <input 
      v-model="text"
      type="text"
      placeholder="Add todo"
      class="border p-2 w-full" 
    />
  </form>
</template>

<script lang="ts">
import { ref } from 'vue'

export default {
  setup(props, { emit }) {
    const text = ref<string>('')

    function onSubmit() {
      emit('add-todo', text.value)
      text.value = ''
    }

    return {
      text,
      onSubmit
    }
  }
}
</script>