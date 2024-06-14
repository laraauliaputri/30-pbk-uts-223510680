<template>
  <div class="post-container">
    <h2 class="post-title">Post</h2>
    <select v-model="selectedUser" @change="fetchPosts" class="post-select">
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>
    <transition-group name="fade">
      <div v-for="post in posts" :key="post.id" class="post-item">
        <h3 class="post-item-title">{{ post.title }}</h3>
        <p class="post-item-body">{{ post.body }}</p>
      </div>
    </transition-group>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
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
};
</script>

<style scoped>
.post-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background-color: #f0f8ff; /* Alice blue background color */
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.post-title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 28px;
  color: #4682b4;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.post-select {
  display: block;
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  border: 2px solid #4682b4; /* Steel blue border */
  border-radius: 5px;
  font-size: 18px;
  color: #2e8b57; /* Sea green text color */
  background-color: #f0ffff; /* Light cyan background */
}

.post-item {
  margin-bottom: 20px;
}

.post-item-title {
  font-size: 24px;
  margin-bottom: 10px;
  color: #191970;
  font-weight: bold; /* Teks tebal */
  transition: color 0.3s ease;
}

.post-item-title:hover {
  color: #4169e1; /* Royal blue text color on hover */
}

.post-item-body {
  font-size: 16px;
  color: #556b2f; /* Dark olive green text color */
  font-style: italic; /* Teks miring */
}
</style>
