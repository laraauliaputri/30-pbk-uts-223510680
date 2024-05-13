<script setup>
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
import { ref, onMounted } from 'vue';

const selectedUser = ref(null);
const users = ref([]);
const posts = ref([]);
const selectedUserName = ref('');

const fetchUsers = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    users.value = await response.json();
  } catch (error) {
    console.error('Error fetching users:', error);
  }
};

const fetchPosts = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await response.json();
  } catch (error) {
    console.error('Error fetching posts:', error);
  }
};

const fetchTodos = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    posts.value = await response.json();
  } catch (error) {
    console.error('Error fetching todos:', error);
  }
};

onMounted(fetchUsers);

const handlePostClick = async () => {
  await fetchPosts();
  selectedUser.value = 'post';
};

const handleTodosClick = async () => {
  await fetchTodos();
  selectedUser.value = 'todos';
};
</script>

<template>
  
</template>
