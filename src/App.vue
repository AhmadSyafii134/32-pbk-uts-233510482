<template>
  <div class="app">
    <h1 class="title">Daftar Kegiatan</h1>
    <form @submit.prevent="addTodo" class="todo-form">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." required />
      <button type="submit">Tambah</button>
    </form>

    <div class="todo-columns">
      <div class="todo-section">
  <h2>Belum Selesai</h2>
  <ul class="todo-list">
    <li v-if="incompleteTodos.length === 0" class="todo-item empty-message">
      Tidak ada Kegiatan
    </li>
    <transition-group v-else name="fade" tag="ul" class="todo-list">
      <li
        v-for="(todo, index) in incompleteTodos"
        :key="todo.text + index"
        class="todo-item"
      >
        <span @click="toggleComplete(index)">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Hapus</button>
      </li>
    </transition-group>
  </ul>
</div>

      <div class="todo-section">
        <h2>DiSelesaikan</h2>
        <transition-group name="complete" tag="ul" class="todo-list">
          <li
            v-for="(todo, index) in completeTodos"
            :key="todo.text + index"
            class="todo-item"
          >
            <span class="done" @click="toggleComplete(index)">{{ todo.text }}</span>
            <button @click="removeTodo(index)">Hapus</button>
          </li>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
    };
  },
  computed: {
    incompleteTodos() {
      return this.todos.filter((t) => !t.completed);
    },
    completeTodos() {
      return this.todos.filter((t) => t.completed);
    },
  },
  methods: {
    addTodo() {
      this.todos.push({ text: this.newTodo, completed: false });
      this.newTodo = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleComplete(index) {
      this.todos[index].completed = !this.todos[index].completed;
    },
  },
};
</script>

<style scoped>
.app {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Inter', sans-serif;
  background-color: #111;
  color: #f5f5f5;
  border-radius: 20px;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.05);
}

.title {
  text-align: center;
  font-size: 2.5rem;
  color: gold;
  margin-bottom: 2rem;
  font-weight: 600;
}

.todo-form {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
}

.todo-form input {
  flex: 1;
  padding: 0.75rem;
  border: none;
  border-radius: 8px;
  background-color: #222;
  color: #fff;
  font-size: 1rem;
  outline: none;
}

.todo-form button {
  padding: 0.75rem 1rem;
  background-color: gold;
  border: none;
  border-radius: 8px;
  color: #111;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.todo-form button:hover {
  background-color: #e0c200;
}

.todo-columns {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  flex-wrap: wrap;
}

.todo-section {
  flex: 1;
  background-color: #1a1a1a;
  padding: 1rem;
  border-radius: 10px;
}

.todo-section h2 {
  text-align: center;
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: #f5f5f5;
  border-bottom: 1px solid #333;
  padding-bottom: 0.5rem;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  background-color: #222;
  padding: 0.75rem 1rem;
  margin-bottom: 0.75rem;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: background-color 0.3s ease;
}

.todo-item:hover {
  background-color: #333;
}

.todo-item span {
  cursor: pointer;
  font-size: 1rem;
}

.todo-item span.done {
  text-decoration: line-through;
  color: #888;
  font-style: italic;
}

.todo-item button {
  background: none;
  border: none;
  color: #f55;
  font-weight: bold;
  cursor: pointer;
  transition: color 0.3s ease;
}

.todo-item button:hover {
  color: #ff9999;
}

/* Animasi Masuk & Keluar */
.fade-enter-active,
.complete-enter-active {
  transition: all 0.4s ease;
}
.fade-leave-active,
.complete-leave-active {
  transition: all 0.3s ease;
  opacity: 0;
  transform: translateY(20px);
}
.fade-enter-from,
.complete-enter-from {
  opacity: 0;
  transform: translateY(-20px);
}
.fade-leave-to,
.complete-leave-to {
  opacity: 0;
  transform: scale(0.9);
}
</style>
