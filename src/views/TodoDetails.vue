<script setup lang="ts">
import { getTodoById } from '@/api/todo-api'
import IconBack from '@/components/icons/IconBack.vue'
import { useQuery } from '@tanstack/vue-query'
import { useRoute } from 'vue-router'

const route = useRoute()

const { data } = useQuery({
  queryKey: ['todo', route.params.id],
  queryFn: () => getTodoById(route.params.id as string)
})
</script>

<template>
  <div class="mt-4 max-w-lg mx-auto p-4 bg-white shadow rounded">
    <h2 class="text-2xl font-bold mb-4 flex items-center">
      <router-link to="/" class="mr-2 text-gray-500 hover:text-gray-800">
        <IconBack />
      </router-link>
      Edit TODO
    </h2>

    <form>
      <div class="mb-4">
        <label for="title" class="block text-gray-700 mb-2">Title</label>
        <input
          :value="data?.title"
          type="text"
          id="title"
          class="w-full p-2 border border-gray-300 rounded"
        />
      </div>
      <div class="mb-4">
        <label for="description" class="block text-gray-700 mb-2">Description</label>
        <textarea
          :value="data?.description"
          id="description"
          class="w-full p-2 border border-gray-300 rounded"
        ></textarea>
      </div>
      <div class="mb-4">
        <button type="button" class="p-2 bg-yellow-500 text-white rounded">Add to favorites</button>
      </div>
      <button type="submit" class="p-2 bg-blue-500 text-white rounded">Save</button>
    </form>
  </div>
</template>
