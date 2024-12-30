<template>
  <div id="particles-js"></div>
  <div class="content">
    <h1>Добро пожаловать в Canfly</h1>
    <p>
      Canfly создает и изучает искусственный интеллект (AI), приветствуя рассвет новой эры — эры, где AI не только существует, но и процветает в мирах, созданных из слияния реальности и фантазии. Мы стремимся создавать цифровые царства, наполненные эстетичными пейзажами, которые кажутся вырванными из снов.
    </p>
    <div class="signature">
      Adiom Timur
    </div>
    <div class="social-icons">
      <a href="https://github.com/yourusername" target="_blank" aria-label="GitHub"><i class="fab fa-github"></i></a>
      <a href="https://twitter.com/yourusername" target="_blank" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
      <a href="https://facebook.com/yourusername" target="_blank" aria-label="Facebook"><i class="fab fa-facebook-f"></i></a>
      <a href="https://flickr.com/yourusername" target="_blank" aria-label="Flickr"><i class="fab fa-flickr"></i></a>
    </div>
  </div>
</template>

<script>
import { onMounted } from 'vue';
import particlesJS from 'particles.js';

export default {
  name: 'Content',
  setup() {
    onMounted(() => {
      particlesJS.load('particles-js', '/particles.json', function () {
        console.log('Particles.js загружен!');
      });
    });
  }
};
</script>

<style scoped>
/* Вставьте сюда ваши стили */
</style>