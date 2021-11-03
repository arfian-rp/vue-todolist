<template>
  <div class="container mt-4 mb-4">
    <div class="row">
      <ul class="list-group">
        <li class="list-group-item" v-for="(todo, i) in todos" :key="i">
          <div class="row">
            <div class="col">
              <span v-if="todo.isDone"
                ><del>{{ todo.activity }}</del></span
              >
              <span v-else>{{ todo.activity }}</span>
            </div>
            <div class="col-auto">
              <div class="row gx-1 flex">
                <div class="col">
                  <button class="btn btn-info" v-if="!todo.isDone" @click="done(i)">
                    <i class="bi bi-check2-square"></i>
                  </button>
                  <button class="btn btn-info" v-else @click="unDone(i)">
                    <i class="bi bi-x-square"></i>
                  </button>
                </div>
                <div class="col">
                  <button class="btn btn-danger" @click="deleteTodo(i)"><i class="bi bi-trash"></i></button>
                </div>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  emits: ["delTodo", "doneTodo"],
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },
  methods: {
    deleteTodo(i) {
      this.$emit("delTodo", i);
    },
    done(i) {
      this.$emit("doneTodo", [i, true]);
    },
    unDone(i) {
      this.$emit("doneTodo", [i, false]);
    },
  },
};
</script>

<style>
.form-check-input {
  margin-top: -0.2px;
  margin-right: 5px;
  width: 2.5rem;
  height: 2.5rem;
  border: 1px solid black;
}
.btn {
  width: 2.6rem;
  height: 2.6rem;
}
.bi {
  margin-left: -0.2rem;
  font-size: 1.2rem;
}
</style>
