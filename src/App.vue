<template>
  <div class="app">
    <h1>📋 List Kegiatan</h1>

    
    <form @submit.prevent="addTask" class="form">
      <input
        v-model="newTask"
        type="text"
        placeholder="Masukkan kegiatan baru..."
        class="input"
      />
      <button type="submit" class="btn-add">➕ Tambah</button>
    </form>

    
    <div class="filter-buttons">
      <button @click="filter = 'all'" :class="{ active: filter === 'all' }">
        Semua
      </button>
      <button @click="filter = 'unfinished'" :class="{ active: filter === 'unfinished' }">
        Belum Selesai
      </button>
    </div>

   
    <transition-group name="task-list" tag="ul" class="task-list">
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
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'all',  
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

body {
  background-color: #e0f7fa; 
  font-family: 'Poppins', sans-serif;
}


.app {
  max-width: 500px;
  margin: 80px auto;
  background: #ffffff;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
  text-align: center;
  animation: fadeIn 0.8s ease; 
}


h1 {
  font-size: 30px;
  margin-bottom: 24px;
  color: #00796b; 
  animation: slideDown 0.6s ease;
}


.form {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
}

.input {
  flex: 1;
  padding: 12px;
  border: 2px solid #80deea;
  border-radius: 12px;
  font-size: 16px;
  outline: none;
  transition: 0.3s;
}

.input:focus {
  border-color: #00acc1;
}

.btn-add {
  background-color: #00acc1;
  color: white;
  border: none;
  padding: 12px 18px;
  font-size: 16px;
  border-radius: 12px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-add:hover {
  background-color: #00838f;
}


.filter-buttons {
  margin-bottom: 20px;
}

.filter-buttons button {
  margin: 0 5px;
  padding: 8px 14px;
  border: none;
  border-radius: 8px;
  background-color: #b2ebf2;
  cursor: pointer;
  transition: background-color 0.3s;
}

.filter-buttons .active {
  background-color: #00acc1;
  color: white;
}


.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  background: #ffffff;
  margin-bottom: 12px;
  padding: 14px 20px;
  border-radius: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s;
  animation: scaleUp 0.5s ease;
}

.task-item:hover {
  background: #e0f2f1;
}

.completed {
  background-color: #b2dfdb;
}

.completed .task-text {
  text-decoration: line-through;
  color: gray;
  opacity: 0.7;
}


.task-content {
  display: flex;
  align-items: center;
  gap: 10px;
}


.check-icon {
  color: #00acc1;
  font-size: 18px;
}


.btn-cancel {
  background-color: #ff8a80;
  border: none;
  color: white;
  padding: 8px 12px;
  font-size: 14px;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-cancel:hover {
  background-color: #e53935;
}


@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes scaleUp {
  from {
    transform: scale(0.95);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
