<template>
  <div>
    <h2 style="color: #87ceeb; text-align: center; font-weight: bold; font-family: cursive; ">Albums</h2>
    <div v-if="albums.length">
      <table class="album-table">
        <tbody>
          <tr v-for="album in albums" :key="album.id" @click="viewAlbum(album.id)" class="album-item" style="cursor: pointer;">
            <td class="album-id">{{ album.id }}</td>
            <td class="album-title">{{ album.title }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else style="text-align: center; margin-top: 20px;">
      <p>No albums available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useAlbumsStore } from '../stores/albums'
import { useRouter } from 'vue-router'

const albumsStore = useAlbumsStore()
const albums = ref([])
const router = useRouter()

const fetchAlbums = async () => {
  await albumsStore.fetchAlbums()
  albums.value = albumsStore.albums
}

const viewAlbum = (id) => {
  router.push(`/albums/${id}`)
}

onMounted(fetchAlbums)
</script>

<style>
.album-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 10px;
}

.album-item {
  transition: background-color 0.3s, color 0.3s, transform 0.3s;
}

.album-item:hover {
  background-color: #add8e6; /* Baby blue background on hover */
  color: #ffffff; /* White text on hover */
  transform: scale(1.02); /* Slightly enlarge on hover */
  box-shadow: 0 4px 15px rgba(0, 123, 255, 0.4); /* Shadow effect on hover */
}

.album-id, .album-title {
  padding: 10px;
  border: 1px solid #87ceeb; /* Light blue border */
  border-radius: 8px; /* Rounded corners */
  transition: background-color 0.3s, border-color 0.3s, color 0.3s; /* Smooth transition for background, border, and color */
}

.album-id {
  font-weight: bold;
  background-color: #e0f7fa; /* Light cyan background for a unique look */
  color: #007bff; /* Darker blue text */
  text-align: center; /* Center align text */
}

.album-title {
  font-family: 'New Romantics', cursive;
  background-color: #f0f8ff; /* Alice blue background */
  color: #005b99; /* Darker shade of blue text */
}

.album-id:hover, .album-title:hover {
  border-color: #76b4bd; /* Darker shade of baby blue border on hover */
  color: #ffffff; /* White text on hover */
  background-color: #87ceeb; /* Baby blue background on hover */
}

.album-id::before {
  content: '#'; /* Add a hash symbol before ID */
  margin-right: 5px;
  color: #007bff;
}

.album-title {
  display: flex;
  align-items: center;
}

.album-title a {
  text-decoration: none; /* Remove underline from links */
  color: inherit; /* Inherit color from parent */
  transition: color 0.3s;
}

.album-title a:hover {
  color: #007bff; /* Change color on hover */
}
</style>
