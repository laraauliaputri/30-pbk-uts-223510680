<template>
  <div class="todo-list-container">
    <header class="header">
      <h1 class="header-title">Daftar Kegiatan</h1>
    </header>
    <div class="todo-form-container">
      <form @submit.prevent="addActivity" class="todo-form">
        <div class="form-group">
          <label for="activity" class="form-label">Kegiatan:</label>
          <input type="text" id="activity" v-model="newActivity" class="form-input">
        </div>
        <div class="form-group">
          <label for="date" class="form-label">Tanggal:</label>
          <input type="date" id="date" v-model="newDate" class="form-input">
        </div>
        <div class="form-group">
          <label for="time" class="form-label">Jam:</label>
          <input type="time" id="time" v-model="newTime" class="form-input">
        </div>
        <div class="form-group">
          <label for="location" class="form-label">Lokasi:</label>
          <input type="text" id="location" v-model="newHobby" class="form-input">
        </div>
        <button type="submit" class="form-button">Daftar</button>
      </form>
    </div>
    <div class="activity-list-container">
      <h2 class="activity-list-title">Daftar Kegiatan</h2>
      <div class="activity-cards">
        <div v-for="(activity, index) in activities" :key="index" class="activity-card">
          <div class="activity-header">
            <input type="checkbox" v-model="activity.completed" @change="toggleCompletion(activity)" class="activity-checkbox">
            <h3 :class="{ 'completed': activity.completed }" class="activity-name">{{ activity.name }}</h3>
          </div>
          <p class="activity-detail">Tanggal: {{ activity.date }}</p>
          <p class="activity-detail">Jam: {{ activity.time }}</p>
          <p class="activity-detail">Lokasi: {{ activity.hobby }}</p>
          <button @click="cancelActivity(index)" class="activity-cancel-button">Batalkan</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      newDate: '',
      newTime: '',
      newHobby: '',
      activities: []
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity && this.newDate && this.newTime && this.newHobby) {
        this.activities.push({
          name: this.newActivity,
          date: this.newDate,
          time: this.newTime,
          hobby: this.newHobby,
          completed: false
        });
        this.newActivity = '';
        this.newDate = '';
        this.newTime = '';
        this.newHobby = '';
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1);
    },
    toggleCompletion(activity) {
      activity.completed = !activity.completed;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.todo-list-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}

.header {
  background: linear-gradient(to right, #ADD8E6, #87CEFA);
  width: 100%;
  padding: 20px 0;
  text-align: center;
  color: white;
  margin-bottom: 20px;
}

.header-title {
  margin: 0;
  font-size: 2.5rem;
}

.todo-form-container {
  max-width: 600px;
  width: 100%;
}

.todo-form {
  background-color: #f0f8ff; /* Warna latar belakang baby blue */
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.2s;
}

.todo-form:hover {
  transform: translateY(-5px);
}

.form-group {
  margin-bottom: 20px;
}

.form-label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #333;
}

.form-input {
  width: calc(100% - 12px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  transition: border-color 0.3s;
}

.form-input:focus {
  border-color: #87CEEB; /* Warna biru muda saat input aktif */
}

.form-button {
  background-color: #87CEFA; /* Warna latar biru muda */
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.form-button:hover {
  background-color: #76b4bd; /* Warna biru yang lebih gelap saat hover */
}

.activity-list-container {
  margin-top: 20px;
  width: 100%;
  text-align: center;
}

.activity-list-title {
  font-size: 1.5rem;
  color: #333; /* Warna teks lebih gelap */
}

.activity-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.activity-card {
  background-color: #f0f8ff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.2s;
  width: calc(100% / 3 - 20px); /* Tiga kartu per baris */
  box-sizing: border-box;
}

.activity-card:hover {
  transform: translateY(-5px);
}

.activity-header {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.activity-checkbox {
  margin-right: 10px;
}

.activity-name {
  font-weight: bold;
  color: #333;
  margin: 0;
}

.activity-detail {
  margin: 5px 0;
  color: #666;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.activity-cancel-button {
  background-color: #dc3545;
  color: #fff;
  padding: 6px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.activity-cancel-button:hover {
  background-color: #c82333;
}

@media (max-width: 768px) {
  .activity-card {
    width: calc(100% / 2 - 20px); /* Dua kartu per baris */
  }
}

@media (max-width: 480px) {
  .activity-card {
    width: 100%; /* Satu kartu per baris */
  }
}
</style>
