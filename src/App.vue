<template>
  <div class="container">
    <h1><img src="./assets/logo.png" alt="Vue logo" width="10%" /> To Do</h1>
    <create-todo
      @add-todo="addTodo($event)"
      :newId="todos[todos.length - 1].id + 1"
    />

    <div class="row">
      <ul>
        <todo
          v-for="(todo, index) in todos"
          :key="index"
          :id="todo.id"
          :isComplete="todo.isComplete"
          :text="todo.text"
          @toggle-todo="toggleTodo(todo)"
          @edit-todo="editTodo(todo, $event)"
          @delete-todo="deleteTodo(todo)"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import CreateTodo from "./components/CreateTodo";
import Todo from "./components/Todo";

export default {
  name: "App",
  components: {
    CreateTodo,
    Todo,
  },
  data() {
    return {
      todos: [
        {
          id: 0,
          isComplete: true,
          text: "Lorem Ipsum",
        },
        {
          id: 1,
          isComplete: false,
          text: "Learn Vue.js",
        },
      ],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    toggleTodo(todo) {
      todo.isComplete = !todo.isComplete;
    },
    editTodo(todo, editedText) {
      todo.text = editedText;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter((todo) => todo !== deletedTodo);
    },
  },
};
</script>

<style>
.container {
  width: 50%;
  margin-top: 50px;
}

h1 {
  text-align: center;
}

ul {
  list-style: none;
  width: 100%;
}
</style>
