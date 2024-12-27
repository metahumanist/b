<template>
  <div class="container">
    <h1 class="title">Welcome to Canfly</h1>
    <ul class="authors-list">
      <li v-for="author in authors" :key="author._path" class="author-item">
        <NuxtLink :to="author._path.replace('/authors/', '/')" class="author-link">
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

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
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