<script setup>
import { Icon } from '@iconify/vue'

const props = defineProps({
  todo: {
    type: Object,
    required: true
  },
  idx: {
    type: Number,
    required: true
  }
})

defineEmits(['toggle-completed', 'edit-todo', 'update-todo', 'delete-todo'])
</script>

<template>
  <li
    :class="[
      'grid grid-cols-3 px-4 py-2 cursor-pointer rounded-md my-2 group shadow-md',
      todo.isCompleted ? 'bg-gray-500' : 'bg-green-200'
    ]"
  >
    <div class="flex space-x-2 items-center col-span-2">
      <p class="text-[10px]">{{ idx + 1 }}:</p>
      <input
        type="checkbox"
        :checked="todo.isCompleted"
        class="cursor-pointer"
        @input="$emit('toggle-complete', idx)"
      />
      <div class="join">
        <input
          v-if="todo.isEditing"
          type="text"
          :value="todo.todo"
          class="rounded text-gray-500 px-2 text-sm"
          @input="$emit('update-todo', $event.target.value, idx)"
        />
        <h1 v-else :class="['text-sm', todo.isCompleted && 'line-through']">{{ todo.todo }}</h1>
      </div>
    </div>
    <div
      class="group-hover:opacity-100 opacity-0 transition-all ease-in-out duration-500 flex justify-end items-center space-x-3"
    >
      <div class="gr">
        <Icon
          v-if="todo.isEditing"
          icon="material-symbols:check-circle-outline"
          color="green"
          class="opacity-50 hover:opacity-100"
          @click="$emit('edit-todo', idx)"
        />
        <Icon
          v-else
          icon="material-symbols:edit-square-outline"
          color="green"
          class="opacity-50 hover:opacity-100"
          @click="$emit('edit-todo', idx)"
        />
      </div>
      <Icon icon="material-symbols:delete" color="red" class="opacity-50 hover:opacity-100" @click="$emit('delete-todo', todo.id)"/>
    </div>
  </li>
</template>

<style scoped></style>
