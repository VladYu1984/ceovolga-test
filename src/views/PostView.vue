<template>
  <div v-if="!post">
    <h1>Постов нет</h1>
  </div>
  <div v-else class="container-post">
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    <router-link to="/">Back to Home</router-link>
  </div>
</template>

<script>
import { IndexedDB } from '../helpers/indexeddb.js';

export default {
  props: ['id'],
  data() {
    return {
      post: {},
    };
  },
  async created() {
    await this.loadPost();
  },
  methods: {
    async loadPost() {
      const db = await new IndexedDB('stateDB', 1); // Создание экземпляра IndexedDB

      // Получение данных по id из IndexedDB
      this.post = await db.get('state', `post_${this.id}`);
    },
  },
};
</script>

<style scoped>
  .container-post p {
    margin-bottom: 30px;
  }
</style>