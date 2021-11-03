<template>
  <div class="container">
    <div class="card pt-3">
      <div class="card-body">
        <h5 class="card-title">VUE 3 TODOLIST APP</h5>
        <div class="small">
          <div>Total: {{ todos.length }}</div>
          <div>
            Created by <a href="https://arfian-id.web.app" target="_blank"><i>Arfian</i></a>
          </div>
        </div>
        <div class="row">
          <div class="col-10">
            <input type="text" autofocus class="form-control" v-model="todoInput" @keyup.enter="add" />
          </div>
          <div class="col-2">
            <button class="btn btn-success" @click="add"><i class="bi bi-plus"></i></button>
          </div>
        </div>
        <List :todos="todos" @delTodo="delTodo" @doneTodo="doneTodo" />
      </div>
    </div>
  </div>
</template>

<script>
import List from "./components/List.vue";

export default {
  name: "App",
  components: { List },
  data() {
    return {
      status: "true",
      todoInput: "",
      todos: [],
    };
  },
  beforeMount() {
    if (localStorage.getItem("TODOS")) {
      this.todos = JSON.parse(localStorage.getItem("TODOS"));
    } else {
      localStorage.setItem("TODOS", "[]");
    }
  },
  updated() {
    localStorage.setItem("TODOS", JSON.stringify(this.todos));
  },
  methods: {
    add() {
      if (this.todoInput) {
        this.todos.unshift({
          activity: this.todoInput,
          isDone: false,
        });
        this.todoInput = "";
      }
    },
    delTodo(i) {
      this.todos.splice(i, 1);
    },
    doneTodo([i, v]) {
      this.todos[i].isDone = v;
      localStorage.setItem("TODOS", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
.small {
  display: flex;
  font-size: small;
}
.small div {
  margin-right: 2rem;
  margin-bottom: 5px;
}
a {
  text-decoration: none;
}
</style>
