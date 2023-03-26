<script setup>
import { ref, defineEmits, reactive } from 'vue'
import TodoButton from '../components/TodButton.vue'
const emit = defineEmits(['create-todo'])

const todoState = reactive({
  todo: '',
  invalid: null,
  errMsg: ''
})

const createTodo = () => {
  todoState.invalid = null
  if (todoState.todo !== '') {
    emit('create-todo', todoState.todo)
    todoState.todo = ''
    return
  }
  todoState.invalid = true
  todoState.errMsg = 'Todo value cannot be empty'
}
</script>

<template>
  <div class="p-4 flex justify-center">
    <div
      :class="[
        'flex justify-between items-center pl-2 py-1 rounded-md shadow w-64 border',
        todoState.invalid ? 'border-red-500' : ''
      ]"
    >
      <input
        type="text"
        @keyup.enter="createTodo()"
        v-model="todoState.todo"
        placeholder="Enter todo"
        class="placeholder:text-[10px] focus:outline-none text-sm w-full"
      />
      <TodoButton @click="createTodo()" />
    </div>
  </div>
  <p v-show="todoState.invalid" class="text-red-500 text-[10px] text-center">
    {{ todoState.errMsg }}
  </p>
</template>


