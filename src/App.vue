<template>
  <div id="app">
    <h1>Kegiatan Hari Ini</h1>
    <div class="input-container">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambahkan kegiatan baru...">
      <button @click="addTask">Tambahkan</button>
    </div>
    <div v-for="(task, index) in tasks" :key="index" class="activity-item">
      <span :class="{ completed: task.completed }" v-if="!task.editing">{{ task.name }}</span>
      <input v-model="task.name" v-else @keyup.enter="saveEdit(index)">
      <div class="buttons">
        <button @click="toggleCompletion(index)">{{ task.completed ? 'Batal' : 'Selesai' }}</button>
        <button @click="deleteTask(index)">Hapus</button>
        <button @click="editTask(index)">{{ task.editing ? 'Simpan' : 'Edit' }}</button>
      </div>
    </div>
    <button @click="showIncomplete" class="clear-completed">Hapus Semua Kegiatan Selesai</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ name: this.newTask, completed: false, editing: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    showIncomplete() {
      this.tasks = this.tasks.filter(task => !task.completed);
    },
    editTask(index) {
      this.tasks.forEach((task, i) => {
        if (i === index) {
          task.editing = !task.editing;
        } else {
          task.editing = false;
        }
      });
    },
    saveEdit(index) {
      this.tasks[index].editing = false;
    }
  }
}
</script>

<style scoped>
#app {
  font-family: 'Arial', sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #2c3e50;
  border-radius: 10px;
  box-shadow: 0px 4px 8px rgba(244, 244, 244, 0.1);
}

h1 {
  text-align: center;
  color: #ecf0f1;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

.input-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #7f8c8d;
  border-radius: 5px;
  margin-right: 10px;
  background-color: #34495e;
  color: #ecf0f1;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

button {
  padding: 10px 15px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2980b9;
}

.activity-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #7f8c8d;
  padding: 10px 0;
}

.activity-item:last-child {
  border-bottom: none;
}

.completed {
  text-decoration: line-through;
  color: #95a5a6;
}

.buttons {
  display: flex;
  gap: 10px;
}

button {
  background-color: #3498db;
  color: white;
}

button:hover {
  background-color: #2980b9;
}

.clear-completed {
  background-color: #e74c3c;
  color: white;
  margin-top: 20px;
}

.clear-completed:hover {
  background-color: #c0392b;
}
</style>
