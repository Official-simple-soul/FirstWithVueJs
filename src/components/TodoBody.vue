<script setup>
import { ref, watch, computed } from 'vue'
import SearchBox from './SearchBox.vue'
import { uid } from 'uid'
import TodoItem from './TodoItem.vue'

const todoList = ref([])

watch(
  todoList,
  () => {
    setTodoLocalStorage()
  },
  {
    deep: true
  }
)

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
}

const toggleComplete = (pos) => {
  todoList.value[pos].isCompleted = !todoList.value[pos].isCompleted
}
const editTodo = (pos) => {
  todoList.value[pos].isEditing = !todoList.value[pos].isEditing
}

const updateTodo = (val, pos) => {
  todoList.value[pos].todo = val
}

const deleteTodo = (id) => {
  todoList.value = todoList.value.filter((e) => e.id !== id)
}
const getTodo = () => {
  const getIt = JSON.parse(localStorage.getItem('todo'))
  if (getIt) {
    todoList.value = getIt
  }
}
getTodo()
const setTodoLocalStorage = () => {
  localStorage.setItem('todo', JSON.stringify(todoList.value))
}
const checkCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted)
})
</script>

<template>
  <div class="">
    <SearchBox @create-todo="createTodo" />
  </div>
  <ul v-if="todoList.length > 0" class="px-3">
    <TodoItem
      v-for="(todo, idx) in todoList"
      v-bind:key="idx"
      :todo="todo"
      :idx="idx"
      @toggle-complete="toggleComplete"
      @edit-todo="editTodo"
      @update-todo="updateTodo"
      @delete-todo="deleteTodo"
    />
  </ul>
  <h1 v-else class="text-center">Nothing added to your todo</h1>
  <p v-if="checkCompleted && todoList.length>0" class="text-center mt-20 block">Nice!! all your todos is completed</p>
</template>

<style lang="scss" scoped></style>
