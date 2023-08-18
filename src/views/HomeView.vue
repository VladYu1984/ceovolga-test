<template>
  <div class="posts">
    <h1>List of posts</h1>
    <div v-if="isLoading" class="loader"></div>
    <ul>
      <li v-for="post in posts" :key="post.id">
        <router-link :to="{ name: 'post', params: { id: post.id } }">{{ post.title }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import { State } from '../helpers/state.js';

export default {
  data() {
    return {
      posts: [],
      isLoading: false,
    };
  },
  async created() {
    await this.fetchAndSavePosts();
  },
  methods: {
    async fetchAndSavePosts() {
      try {
        this.isLoading = true;
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const data = await response.json();

        const state = new State();
        for (const post of data) {
          await state.set(`post_${post.id}`, post);
        }

        this.posts = data;
      } finally {
        this.isLoading = false;
      }
    },
  },
};
</script>

<style scoped>
  .posts {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
  }

  h1 {
    display: flex;
    justify-content: center;
    font-size: 2.5em;
  }

  a {
    width: 100%;
    margin: 0;
    border-radius: 15px;
  }

  li {
    list-style: none;
    /* padding: 10px 0; */

    font-size: 1.5em;
    border: 1px solid black;
    border-radius: 15px;
    margin: 15px 0;
    background-color: rgba(249, 208, 154, 0.665);
    color: rgb(79, 79, 79);

    cursor: pointer;

    display: flex;
    justify-content: center;
  }

  li:hover {
    background-color: rgb(255, 89, 0);
    color: #fff;
  }

  button .btn {
    display: flex;
    margin: 0 auto;
    align-items: center;
  }

  button:disabled {
    background-color: transparent;
    border: none;
  }

  .loader {
      position: absolute;
      top: 150px;
      border: 4px solid #f3f3f3;
      border-top: 4px solid #3498db;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 2s linear infinite;
      margin: 0;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
</style>