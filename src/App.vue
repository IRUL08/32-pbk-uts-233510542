<template>
  <div class="app">
    <h1>My To-Do List</h1>

    <!-- Input untuk menambahkan kegiatan -->
    <form @submit.prevent="addTask">
      <input v-model="newTask" placeholder="Tambah kegiatan baru..." />
      <button type="submit">Tambah</button>
    </form>

    <!-- Daftar kegiatan -->
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',    // Untuk input baru
      tasks: [],      // Daftar kegiatan
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask.trim()) // Tambahkan ke array
        this.newTask = ''                    // Kosongkan input setelah tambah
      }
    },
  },
}
</script>

<style scoped>
.app {
  max-width: 500px;
  margin: 50px auto;
  text-align: center;
}
input {
  width: 70%;
  padding: 10px;
  margin-right: 5px;
}
button {
  padding: 10px 20px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin: 10px 0;
  background: #f0f0f0;
  padding: 10px;
  border-radius: 5px;
}
</style>
