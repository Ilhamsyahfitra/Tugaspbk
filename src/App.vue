<template>
  <div id="app">
    <h1>Kegiatan hari ini</h1>
    <input v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">tambahkan kagiatan</button>
    <div v-for="(task, index) in tasks" :key="index">
      <span :class="{ completed: task.completed }">{{ task.name }}</span>
      <button @click="toggleCompletion(index)">selesai</button>
      <button @click="deleteTask(index)">hapus</button>
    </div>
    <button @click="showIncomplete">Hapus semua kegiatan selesai</button>
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
      this.tasks.push({ name: this.newTask, completed: false });
      this.newTask = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    showIncomplete() {
      this.tasks = this.tasks.filter(task => !task.completed);
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  
}

#app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  max-height: 900px;
  margin: 0 auto;
  padding: 20px;
  background-color: #039c3b;
  border-radius: 20px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

input, button {
  background-color: rgb(255, 255, 255);
  padding: 5px;
  font-size: 16px;
  border: none;
  margin-bottom: 10px;
}

button {
  background-color: rgb(0, 0, 0);
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: rgba(255, 0, 0, 0.636);
}

.completed {
  text-decoration: line-through;
  color: #422626;
}

.activity-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
}

.activity-item:last-child {
  border-bottom: none;
}

</style>