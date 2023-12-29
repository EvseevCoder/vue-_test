<template>
  <ul class="todo-list">
    <AppTodoitem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppTodoitem from "./AppTodoitem.vue";
import type { Todo } from "@/types/Todo";

export default defineComponent({
  components: {
    AppTodoitem,
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
    },
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit("toggleTodo", id);
    },
    removeTodo(id: number) {
      this.$emit("removeTodo", id);
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
});
</script>
