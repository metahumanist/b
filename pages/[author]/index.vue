<template>
  <div v-if="author" class="p-4">
    <div class="mb-8">
      <a href="https://canfly.org/" class="text-blue-500 hover:underline">
        Canfly
      </a>
      <h1 class="text-3xl font-bold">My name is {{ author.name }}</h1>
      <p class="text-gray-600">{{ author.bio }}</p>
    </div>

    <div class="posts">
      <h2 class="text-2xl font-bold mb-4">Posts</h2>
      <div v-if="posts.length" class="space-y-4">
        <article v-for="post in posts" :key="post._path" class="border p-4 rounded">
          <h3 class="text-xl font-semibold">{{ post.title }}</h3>
          <p class="text-gray-500">{{ new Date(post.date).toLocaleDateString() }}</p>
          <p class="mt-2">{{ post.description }}</p>
          <NuxtLink :to="`/${authorSlug}/${post._path.split('/').pop()}`" class="text-blue-500 hover:underline">
            Read more
          </NuxtLink>
        </article>
      </div>
      <p v-else>No posts found</p>
    </div>
  </div>
  <div v-else>
    <h1>Author not found</h1>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()
const authorSlug = route.params.author as string

const { data: author } = await useAsyncData(`author-${authorSlug}`, () => {
  return queryContent('authors').where({ _path: `/authors/${authorSlug}` }).findOne()
})

const { data: posts } = await useAsyncData(`posts-${authorSlug}`, () => {
  return queryContent('posts')
    .where({ author: authorSlug })
    .sort({ date: -1 })
    .find()
})

definePageMeta({
  title: computed(() => author.value?.name || 'Author')
})
</script>

<style scoped>
div {
  padding: 2rem;
}
</style>
