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

    <!-- Filter Button -->
    <div class="filter-buttons">
      <button @click="filter = 'all'" :class="{ active: filter === 'all' }">
        Semua
      </button>
      <button @click="filter = 'unfinished'" :class="{ active: filter === 'unfinished' }">
        Belum Selesai
      </button>
    </div>

    <!-- Daftar Kegiatan -->
    <ul class="task-list">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="{ completed: task.completed }"
        class="task-item"
      >
        <div class="task-content">
          <input type="checkbox" v-model="task.completed" />
          <span class="check-icon" v-if="task.completed">✔️</span>
          <span class="task-text">{{ task.text }}</span>
        </div>
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
      filter: 'all',  // 'all' atau 'unfinished'
    }
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'unfinished') {
        return this.tasks.filter(task => !task.completed)
      }
      return this.tasks
    }
  },
  methods: {
    addTask() {
      const trimmed = this.newTask.trim()
      if (trimmed) {
        this.tasks.push({ text: trimmed, completed: false })
        this.newTask = ''
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1)
    },
  },
}
</script>

<style scoped>
/* Basic Page Styling */
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

/* Title */
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

/* Filter Buttons */
.filter-buttons {
  margin-bottom: 20px;
}

.filter-buttons button {
  margin: 0 5px;
  padding: 8px 14px;
  border: none;
  border-radius: 8px;
  background-color: #ddd;
  cursor: pointer;
  transition: background-color 0.3s;
}

.filter-buttons .active {
  background-color: #42b983;
  color: white;
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

.completed {
  background-color: #e0f8e9;
}

.completed .task-text {
  text-decoration: line-through;
  color: gray;
  opacity: 0.7;
}

/* Task Content */
.task-content {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* Check Icon */
.check-icon {
  color: #42b983;
  font-size: 18px;
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
