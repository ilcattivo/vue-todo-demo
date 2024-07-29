<script setup lang="ts">
import { getTodos } from '@/api/todo-api'
import IconHeart from '@/components/icons/IconHeart.vue'
import { useQuery } from '@tanstack/vue-query'

const { isPending, isError, data, error } = useQuery({
  queryKey: ['todos'],
  queryFn: getTodos
})
</script>

<template>
  <main>
    <div class="bg-gray-100 min-h-screen w-full flex flex-col items-center p-4">
      <div class="w-full max-w-lg">
        <!-- Header -->
        <header class="mb-6">
          <h1 class="text-3xl font-bold text-center text-gray-800">TODO List</h1>
        </header>

        <!-- Add TODO Form -->
        <div class="mb-4">
          <form class="flex items-center space-x-2">
            <input
              type="text"
              placeholder="Enter title..."
              class="flex-grow p-2 border border-gray-300 rounded"
            />
            <button type="submit" class="p-2 bg-blue-500 text-white rounded">Add</button>
          </form>
        </div>

        <!-- Filter Options -->
        <div class="mb-4 flex justify-end">
          <label class="flex items-center space-x-2">
            <input type="checkbox" id="filter-favorited" class="form-checkbox" />
            <span class="text-gray-700">Show Favorited</span>
          </label>
        </div>

        <!-- TODO List -->
        <span v-if="isPending">Loading...</span>

        <span v-else-if="isError">Error: {{ error?.message }}</span>

        <ul v-if="data" class="space-y-4">
          <!-- TODO Card Template -->
          <li
            v-for="todo of data"
            :key="todo.id"
            class="bg-white p-4 shadow rounded cursor-pointer hover:bg-gray-100"
          >
            <RouterLink :to="{ name: 'todo-details', params: { id: '123' } }">
              <div class="flex justify-between items-center">
                <div>
                  <h2 class="text-xl font-semibold">{{ todo.title }}</h2>
                </div>
                <div>
                  <button class="text-yellow-500">
                    <IconHeart fill="none" />
                  </button>
                </div>
              </div>
            </RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>
