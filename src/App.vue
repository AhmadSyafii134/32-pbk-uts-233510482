<template>
  <div class="card">
    <h1 class="title">Daftar Kegiatan <span class="icon">📋</span></h1>

    <form @submit.prevent="submitTask" class="form">
      <input type="text" v-model="task" placeholder="Tambahkan tugas baru..." class="input" required />
      <button type="submit" class="btn">+ Tambah</button>
    </form>

    <div class="filter-dropdown">
      <button @click="toggleDropdown">
        ⚗️ Filter
      </button>
      <ul v-if="dropdownOpen" class="dropdown-menu">
        <li @click="setFilter('all')">Tampilkan Semua</li>
        <li @click="setFilter('complete')">Tampilkan Selesai</li>
        <li @click="setFilter('incomplete')">Tampilkan Belum Selesai</li>
      </ul>
    </div>

    <ul class="todo-list">
      <li v-if="filteredTasks.length === 0" class="no-task">Belum ada tugas 📭.</li>
      <li v-for="(t, index) in filteredTasks" :key="index" class="task-item">
        <span :class="{ done: t.done }" @click="toggleTask(index)" class="task-text">
          {{ t.text }}
        </span>
        <button @click="removeTask(index)" class="delete-btn">✖</button>
      </li>
    </ul>

    <div class="footer-box">
      <p class="footer">Made by as3_ahmad134</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: '',
      tasks: [],
      filter: 'all',
      dropdownOpen: false,
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'complete') {
        return this.tasks.filter(t => t.done);
      } else if (this.filter === 'incomplete') {
        return this.tasks.filter(t => !t.done);
      }
      return this.tasks;
    }
  },
  methods: {
    submitTask() {
      if (this.task.trim()) {
        this.tasks.push({ text: this.task, done: false });
        this.task = '';
      }
    },
    toggleTask(index) {
      this.tasks[index].done = !this.tasks[index].done;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleDropdown() {
      this.dropdownOpen = !this.dropdownOpen;
    },
    setFilter(value) {
      this.filter = value;
      this.dropdownOpen = false;
    }
  }
};
</script>


<style scoped>
:root {
  --green: #00ff99;
  --dark: #121212;
  --darker: #0d0d0d;
  --gray: #1e1e1e;
}

body {
  margin: 0;
  background-color: var(--dark);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.card {
  background: var(--darker);
  max-width: 400px;
  margin: 60px auto;
  padding: 30px;
  border-radius: 24px;
  box-shadow: 0 0 40px rgba(0, 255, 153, 0.2);
  color: var(--green);
  text-align: center;
}

.title {
  font-size: 24px;
  margin-bottom: 20px;
  font-weight: bold;
}

.icon {
  font-size: 24px;
  margin-left: 8px;
}

.form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.input {
  flex: 1;
  padding: 10px;
  border-radius: 12px;
  border: none;
  background-color: #1f1f1f;
  color: var(--green);
  box-shadow: inset 0 0 5px rgba(0, 255, 153, 0.3);
}

.btn {
  background-color: var(--green);
  color: #00ffa62d;
  border: none;
  border-radius: 12px;
  padding: 10px 20px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 4px 10px rgba(0, 255, 153, 0.3);
}

.filters {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

.filters select {
  background-color: #1f1f1f;
  color: #00ff00;
  border: none;
  border-radius: 10px;
  padding: 8px 16px;
}

.filter-icon {
  font-size: 18px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.task-item {
  background: #1b1b1b;
  margin: 10px 0;
  padding: 10px 16px;
  border-radius: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 0 6px rgba(0, 255, 153, 0.1);
}

.task-text {
  cursor: pointer;
}

.task-text.done {
  text-decoration: line-through;
  color: #777;
  opacity: 0.6;
}

.delete-btn {
  background: transparent;
  border: none;
  color: var(--green);
  font-size: 18px;
  cursor: pointer;
}

.no-task {
  font-style: italic;
  color: #999;
  margin-top: 20px;
}

.footer-box {
  background-color: #1a1a1a;
  padding: 12px;
  border-radius: 12px;
  margin-top: 30px;
  box-shadow: 0 0 10px rgba(0, 255, 153, 0.1);
}

.footer {
  margin: 0;
  font-size: 12px;
  color: #777;
}
</style>

<style scoped>
.filter-dropdown {
  position: relative;
  display: inline-block;
  margin: 1em 0;
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: #1b1b1b;
  border: 1px solid #00ffa62d;
  list-style: none;
  padding: 0.5em;
  margin: 0;
  z-index: 100;
}

.dropdown-menu li {
  cursor: pointer;
  padding: 0.5em;
}

.dropdown-menu li:hover {
  background-color: #00ffa62d;
}

.done {
  text-decoration: line-through;
}
</style>
