<template>
    <div class="post-container">
      <h2 class="post-title">Post</h2>
      <select v-model="selectedUser" @change="fetchPosts" class="post-select">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
      <div v-for="post in posts" :key="post.id" class="post-item">
        <h3 class="post-item-title">{{ post.title }}</h3>
        <p class="post-item-body">{{ post.body }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import { defineComponent, ref, onMounted } from 'vue';
  
  export default defineComponent({
    setup() {
      const users = ref([]);
      const selectedUser = ref(null);
      const posts = ref([]);
  
      const fetchUsers = async () => {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
          if (!response.ok) {
            throw new Error('Failed to fetch users');
          }
          users.value = await response.json();
        } catch (error) {
          console.error(error);
        }
      };
  
      const fetchPosts = async () => {
        if (!selectedUser.value) return;
  
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
          if (!response.ok) {
            throw new Error('Failed to fetch posts');
          }
          posts.value = await response.json();
        } catch (error) {
          console.error(error);
        }
      };
  
      onMounted(fetchUsers);
  
      return { users, selectedUser, posts, fetchPosts };
    }
  });
  </script>
  
  <style scoped>
  .post-container {
    max-width: 600px;
    margin: 40px auto;
    padding: 20px;
    background-color: #ffffff;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .post-title {
    text-align: center;
    margin-bottom: 20px;
    font-size: 24px;
    color: #333;
  }
  
  .post-select {
    display: block;
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }
  
  .post-item {
    margin-bottom: 20px;
  }
  
  .post-item-title {
    font-size: 20px;
    margin-bottom: 10px;
    color: #675720;
  }
  
  .post-item-body {
    font-size: 16px;
    color: #555;
  }
  </style>
  