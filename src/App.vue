<template>
  <div class="app">
    <h1>My To-Do List</h1>

    <!-- Input Form -->
    <form @submit.prevent="addTask" class="form">
      <input
        v-model="newTask"
        type="text"
        placeholder="Masukkan kegiatan baru..."
        class="input"
      />
      <button type="submit" class="btn">Tambah</button>
    </form>

    <!-- Daftar Kegiatan -->
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',   // Input teks user
      tasks: [],     // Daftar kegiatan
    }
  },
  methods: {
    addTask() {
      const trimmed = this.newTask.trim()
      if (trimmed) {
        this.tasks.push(trimmed)  // Tambahkan ke list
        this.newTask = ''         // Kosongkan input
      }
    },
  },
}
</script>

<style scoped>
.app {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  font-family: Arial, sans-serif;
}

.form {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
}

.btn {
  padding: 10px 20px;
  font-size: 16px;
  margin-left: 10px;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  background: #f4f4f4;
  margin: 8px 0;
  padding: 12px;
  border-radius: 5px;
  text-align: left;
}
</style>
