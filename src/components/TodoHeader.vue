<template>
  <header class="bg-white p-2 shadow">
    <nav class="flex justify-between items-center">
      <div class="logo font-bold">HB-2DO</div>
      <ul class="space-x-4">
        <RouterLink to="/" class="">Home</RouterLink>
        <RouterLink to="/about" class="">About</RouterLink>
      </ul>
      <button class="bg-gray-500 border text-white px-3 text-sm rounded-md shadow-md">Simple_Soul</button>
    </nav>
  </header>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>
