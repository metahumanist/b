<template>
  <div v-if="post" class="p-4 container">
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

<style scoped>
.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem;
}

.title {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.authors-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.author-item {
  margin: 1rem 0;
}

.author-link {
  text-decoration: none;
  color: #3498db;
  font-size: 1.2rem;
  transition: color 0.3s ease;
}

.author-link:hover {
  color: #2980b9;
}
</style>