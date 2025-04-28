<template>
  <div class="app">
    <h1>📋 List Kegiatan</h1>

    <!-- Input Form -->
    <form @submit.prevent="addTask" class="form">
      <input
        v-model="newTask"
        type="text"
        placeholder="Masukkan kegiatan baru..."
        class="input"
      />
      <button type="submit" class="btn-add">➕ Tambah</button>
    </form>

    <!-- Daftar Kegiatan -->
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span>{{ task }}</span>
        <button @click="removeTask(index)" class="btn-cancel">❌ Batal</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
    }
  },
  methods: {
    addTask() {
      const trimmed = this.newTask.trim()
      if (trimmed) {
        this.tasks.push(trimmed)
        this.newTask = ''
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1)
    }
  },
}
</script>

<style scoped>
/* Global Styles */
body {
  background-color: #f0f4f8;
  font-family: 'Poppins', sans-serif;
}

/* App Container */
.app {
  max-width: 500px;
  margin: 80px auto;
  background: #ffffff;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Heading */
h1 {
  font-size: 28px;
  margin-bottom: 20px;
  color: #333;
}

/* Form */
.form {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
}

.input {
  flex: 1;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 12px;
  font-size: 16px;
  outline: none;
  transition: 0.3s;
}

.input:focus {
  border-color: #42b983;
}

/* Add Button */
.btn-add {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 12px 18px;
  font-size: 16px;
  border-radius: 12px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-add:hover {
  background-color: #369f6e;
}

/* Task List */
.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  background: #f9fafc;
  margin-bottom: 12px;
  padding: 14px 20px;
  border-radius: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: background 0.3s;
}

.task-item:hover {
  background: #eef2f7;
}

/* Cancel Button */
.btn-cancel {
  background-color: #ff6b6b;
  border: none;
  color: white;
  padding: 8px 12px;
  font-size: 14px;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-cancel:hover {
  background-color: #ff4c4c;
}
</style>
