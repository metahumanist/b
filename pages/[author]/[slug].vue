<template>
  <div v-if="post" class="p-4">
    <article>
      <h1 class="text-3xl font-bold mb-4">{{ post.title }}</h1>
      <div class="text-gray-500 mb-4">
        {{ new Date(post.date).toLocaleDateString() }}
        by <NuxtLink :to="`/${author}`" class="text-blue-500 hover:underline">{{ author }}</NuxtLink>
      </div>
      <div class="prose max-w-none">
        <ContentRenderer :value="post" />
      </div>
    </article>
  </div>
  <div v-else>
    <h1>Post not found</h1>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()
const { author, slug } = route.params

// Изменяем запрос для поиска поста
const { data: post } = await useAsyncData(`post-${author}-${slug}`, () => {
  return queryContent()
    .where({ 
      $and: [
        { _path: { $contains: '/posts/' } },
        { _path: { $contains: slug } },
        { author: author }
      ]
    })
    .findOne()
})

definePageMeta({
  title: computed(() => post.value?.title || 'Post')
})
</script>
