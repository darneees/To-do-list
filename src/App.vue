<script setup>
import { ref, computed } from "vue";

import "./assets/main.css";

let id = 0;

const title = ref("title");
const text = ref("text");
const header = ref("header");
const main = ref("main");
const addTask = ref("addTask");
const textTodo = ref("textTodo");
const hidden = ref("hidden");
const reserved = ref("reserved");

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  <main>
    <section :id="header">
      <h1 :class="title">To-do List</h1>
      <p :class="text">
        I created a to-do list in Vue.js; it's my first time coding a program in
        Vue.js, and I feel very proud of myself. I hope you enjoy my project.
      </p>
    </section>

    <section :id="main">
      <form @submit.prevent="addTodo">
        <input
          v-model="newTodo"
          :class="textTodo"
          placeholder="Write a task here"
        />
        <button :class="addTask">+</button>
      </form>

      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>

      <button @click="hideCompleted = !hideCompleted" :class="hidden">
        {{ hideCompleted ? "Show" : "Hidden" }}
      </button>
    </section>

    <span :class="reserved"><strong>© Douglas Sá</strong>. All rigths reserved.</span>
  </main>
</template>