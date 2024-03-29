<script setup lang="ts">
import type { Media, MediaType } from '~/types'

defineProps<{
  type: MediaType
  item: Media
}>()
</script>

<template>
  <NuxtLink
    :to="`/${item.media_type || type}/${item.id}`" pb2 relative
  >
    <div
      block p1
      class="aspect-10/16"
      transition duration-400
      hover="scale-105 z10"
    >
      <NuxtImg
        v-if="item.poster_path"
        width="400"
        height="600"
        format="webp"
        :src="`/tmdb${item.poster_path}`"
        :alt="item.title || item.name"
        w-full h-full object-cover rounded-md
        :style="{ 'view-transition-name': `item-${item.id}` }"
      />
      <div v-else h-full op10 flex>
        <div i-ph:question ma text-4xl />
      </div>
    </div>
    <div absolute bottom-0 flex flex-col justify-end p-5 bg-gradient-to-t from-black to-transparent transition-all ease-in-out duration-500 lg:opacity-0 rounded-md class="hover:opacity-100 w-[100%] h-[100%]">
      <div mt-2>
      {{ item.title || item.name }}
    </div>
    <div flex text-sm gap-2 items-center>
      <StarsRate w-20 :value="item.vote_average" />
      <div op60>
        {{ formatVote(item.vote_average) }}
      </div>
    </div>
    </div>
  </NuxtLink>
</template>
