<template>
  <h1>イルハムのウェブサイトへようこそ
Iruhamu no u~ebusaito e yōkoso</h1>
  <div>
    <input v-model="newTodo" placeholder="Masukkan Kegiatan">
    <button @click="addTodo">Tambah Kegiatan</button>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan yang sudah selesai' }}</button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
        <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
        <button @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      newTodo: '',
      nextId: 1,
      hideCompleted: false
    }
  },
  computed: {
    visibleTodos() {
      if (this.hideCompleted) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({
          id: this.nextId++,
          text: this.newTodo,
          completed: false
        });
        this.newTodo = '';
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    completeTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = true;
      }
    },
    unCompleteTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = false;
      }
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    }
  }
}
</script>

<style>
  /* Styling untuk kontainer to-do list */
  .container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }

  /* Gaya judul to-do list */
  h1 {
    text-align: center;
    margin-bottom: 20px;
  }

  /* Gaya input field */
  input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    margin-bottom: 10px;
    border-radius: 5px;
    border: 1px solid #ddd;
  }

  /* Gaya tombol */
  button {
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    border: none;
  }

  button:hover {
    background-color: #45a049;
  }

  button:active {
    background-color: #3e8e41;
  }

  /* Gaya daftar tugas */
  ul {
    list-style: none;
    padding: 0;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  /* Gaya teks tugas yang selesai */
  .completed {
    text-decoration: line-through;
  }
</style>
