<template>
  <div class="app-container">
    <div class="button-container">
      <button @click="goToPost" :class="{ active: showPost }">Post</button>
      <button @click="showTodoListForm" :class="{ active: showForm }">TodoList</button>
    </div>
    <div class="content-container">
      <TodoList v-if="showForm" />
      <PostList v-if="showPost" />
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';
import PostList from './components/PostList.vue';

export default {
  components: {
    TodoList,
    PostList
  },
  data() {
    return {
      showForm: false,
      showPost: false
    };
  },
  methods: {
    showTodoListForm() {
      this.showForm = true;
      this.showPost = false;
    },
    goToPost() {
      this.showPost = true;
      this.showForm = false;
    }
  }
}
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background-color: #faf3e0;
  min-height: 100vh; /* Ensures the container covers full viewport height */
}

.button-container {
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  margin: 0 10px;
  background-color: #675720;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-size: 16px;
  transition: background-color 0.3s, transform 0.3s;
}

button:hover {
  background-color: #675720;
  transform: scale(1.05);
}

button.active {
  background-color: #a08645;
  color: #fff;
  font-weight: bold;
}

.content-container {
  width: 100%;
  max-width: 800px; /* Limits the width of the content */
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Adds a subtle shadow */
  transition: all 0.3s ease;
}

.content-container > *:not(:last-child) {
  margin-bottom: 20px; /* Adds space between components */
}
</style>
