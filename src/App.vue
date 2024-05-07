<script setup>
import { ref, computed } from 'vue' // Import ref dan computed dari Vue

let id = 0 // Variabel id untuk menghasilkan ID baru untuk setiap todo

const newTodo = ref('') // Reactive variable untuk menyimpan teks todo baru
const hideCompleted = ref(false) // Menyimpan status untuk menentukan hideCompleted
const todos = ref([ // Daftar todo dengan reactive variable untuk menyimpan semua todo yang selesai
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: false },
  { id: id++  , text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => { // Menghitung daftar todo berdasarkan hideCompleted
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done) // Jika hideCompleted, sembunyikan todo yang selesai
    : todos.value // Jika false, tampilkan semua todo
})

function addTodo() { // Fungsi untuk menambahkan todo baru
  todos.value.push({ id: id++, text: newTodo.value, done: false }) // Tambahkan todo baru, default done false
  newTodo.value = '' // Kosongkan input setelah menambahkan
}

function removeTodo(todo) { // Fungsi untuk menghapus todo
  todos.value = todos.value.filter((t) => t.id !== todo.id) // Hapus todo berdasarkan id
}

</script>

<template>
  <div class="todo-app">
    <!-- Container untuk aplikasi todo -->
    <form @submit.prevent="addTodo" class="todo-form">
      <!-- form untuk menambahkan todo baru -->
      <input v-model="newTodo" required placeholder="new todo" class="todo-input">
      <!-- input untuk teks todo baru -->
      <button type="submit" class="todo-button">Add Todo</button>
      <!-- tombol untuk menambahkan todo -->
    </form>

    <ul class="todo-list">
      <!-- Daftar todo -->
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <!-- Loop untuk menampilkan item todo -->
        <input type="checkbox" v-model="todo.done">
        <!-- kotak centang untuk menandai todo selesai -->
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <!-- teks todo, garis bawah jika selesai -->
        <button @click="removeTodo(todo)" class="delete-button">X</button>
        <!-- tombol untuk menghapus todo -->
      </li>
    </ul>

    <button @click="hideCompleted = !hideCompleted" :class="toggle-completed">
      <!-- Tombol untuk menyembunyikan/menampilkan todo yang selesai -->
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
      <!-- Teks tombol sesuai status -->
    </button>
  </div>
</template>

<style>
.todo-app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #f7f7f7;
}

.todo-form {
  margin-bottom: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  margin-bottom: 10px;
}

.done {
  text-decoration: line-through;
}

.delete-button {
  margin-left: 10px;
  color: red;
  cursor: pointer;
}

.todo-input, .todo-button {
  padding: 8px;
  margin-right: 5px;
}

body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  width: 300px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  width: 300px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
}

label {
  font-weight: bold;
}

input[type="text"],
input[type="number"],
input[type="email"],
textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button[type="submit"] {
  padding: 10px 20px;
  background-color: #007bff; /* Warna biru */
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button[type="submit"]:hover {
  background-color: #0056b3; /* Warna biru lebih gelap saat hover */
}


.toggle-completed {
  padding: 8px;
  background-color: #eee;
  border: none;
  cursor: pointer;
}
</style>  