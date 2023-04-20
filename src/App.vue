<template>
  <div class="todo-list">
    <h1>Aplikasi Monitoring Peminjam Buku</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Masukkan nama buku..." />
      <input type="text" v-model="newPeminjam" placeholder="Masukkan nama peminjam..." />
      <input type="datetime-local" v-model="newDate" />
      <button type="submit" class="tambahkan">Tambahkan</button>
    </form>
    <h2>List Item</h2>
    <div class="tengah">
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.done" />
          <span>{{ todo.text }}</span>
          <span>{{ todo.date }}</span>
          <span :class="{ 'done': todo.done }">({{ todo.peminjam }})</span>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
    </div>
    <footer>
      <p>&copy;Rahayu Frita Windani</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      newPeminjam: '',
      newDate: '',
      todos: []
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0 || this.newPeminjam.trim().length === 0 || !this.newDate) {
        return;
      }
      this.todos.push({
        text: this.newTodo,
        peminjam: this.newPeminjam,
        done: false,
        date: new Date(this.newDate).toLocaleString(),
      });
      this.newTodo = '';
      this.newPeminjam = '';
      this.newDate = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    removeAllTodos() {
      this.todos = [];
    },
  },
};
</script>


<style>
  .todo-list {
    font-family: sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  body {
    background-image: url(https://img.freepik.com/free-vector/hand-drawn-minimal-background_23-2149005485.jpg?size=626&ext=jpg&ga=GA1.2.1938037349.1681991782&semt=ais);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
  }
  .todo-list h1 {
    font-size: 36px;
    margin-bottom: 20px;
    text-align: center;
  }
  .todo-list form {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  .todo-list input[type="text"] {
    flex: 1;
    font-size: 12px;
    padding: 10px;
    border: 2px solid #ccc;
    border-radius: 5px;
  }
  .todo-list input[type="datetime-local"] {
    width: 400px;
    height: 50px;
    font-size: 14 px;
    padding: 10px;
    margin: 10px 0;
    border: 2px solid #ccc;
    border-radius: 5px;
  }
  .todo-list input[type="text"],
  .todo-list input[type="datetime-local"] {
    box-sizing: border-box;
  }
  .todo-list button {
    font-size: 18px;
    padding: 10px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .todo-list button:hover {
    background-color: #E21818;
  }
  .todo-list button.tambahkan {
    margin-left: 10px;
  }
  .todo-list h2 {
    font-size: 24px;
    margin-bottom: 10px;
  }
  .todo-list ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .todo-list li {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .todo-list li span:nth-child(3) {
    font-size: 16px;
    color: #666;
  }
  .todo-list button.remove {
    background-color: #f44336;
    transition: background-color 0.3s ease;
  }
  .todo-list button.remove:hover {
    background-color: #da190b;
  }
  .todo-list button.remove:active {
    background-color: #da190b;
  }
  .done {
    text-decoration: line-through;
  }
</style>