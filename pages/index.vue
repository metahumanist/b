<template>
  <div>
    <h1>Авторы</h1>
    <ul>
      <li v-for="author in authors" :key="author._path">
        <NuxtLink :to="author._path.replace('/authors/', '/')">
          {{ author.name }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
const { data: authors } = await useAsyncData('authors', () => 
  queryContent('authors').find()
)
</script>