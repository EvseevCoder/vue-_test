<template>
  <AppHeader />
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter" />

  <main class="app-main">
    <AppTodoList
      :todos="filteredTodos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <AppAddTodo @add-todo="addTodo" />
  </main>

  <AppFooter :stats="stats" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";

import type { Todo } from "@types/Todo";
import type { filter } from "@types/Filter";
import type { Stats } from "AppFooter";

interface state {
  todos: Todo[];
  activeFilter: "All" | "Active" | "Done";
}

export default defineComponent({
  data(): state {
    return {
      todos: [
        { id: 0, text: "текст первой задачи", completed: true },
        { id: 1, text: "текст третьей задачи", completed: false },
        { id: 2, text: "текст второй задачи", completed: false },
      ],
      activeFilter: "All",
    };
  },
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter,
  },
  methods: {
    addTodo(todo: Todo) {
      console.log(todo);
      this.todos.push(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo) => todo.id === id);

      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id != id);
    },
    setFilter(filter: filter) {
      this.activeFilter = filter;
    },
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case "Active":
          return this.todos.filter((todo) => !todo.completed);
        case "Done":
          return this.todos.filter((todo) => todo.completed);
        case "All":
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.todos.filter((todo) => !todo.completed).length,
        done: this.todos.filter((todo) => todo.completed).length,
      };
    },
  },
});
</script>
