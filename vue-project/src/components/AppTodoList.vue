<template>
    <ul class="todo-list">

      <AppTodoitem
      v-for="todo in todos"
      :key="todo.id"
      :todo='todo'
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"/>

    </ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppTodoitem from './AppTodoitem.vue'
import type { Todo } from '@/types/Todo';

interface state {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppTodoitem
  },
  data(): state {
    return {
      todos: [
        {id: 0, text: 'текст первой задачи', completed: true},
        {id: 1, text: 'текст третьей задачи', completed: false},
        {id: 2, text: 'текст второй задачи', completed: false}
      ]
    }
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find(todo => todo.id === id)

      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id != id)

    }
  }
})
</script>