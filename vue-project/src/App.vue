<template>
  <AppHeader/>
  <AppFilters/>
  
  <main class="app-main">
    <AppTodoList :todos="todos" @toggle-todo="toggleTodo" @remove-todo="removeTodo"/>
    <AppAddTodo @add-todo="addTodo"/>
  </main>

  <AppFooter/>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppHeader from './components/AppHeader.vue';
import AppFilters from './components/AppFilters.vue';
import AppTodoList from './components/AppTodoList.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter from './components/AppFooter.vue';

import type { Todo } from '@types/Todo';

interface state {
  todos: Todo[]
}


export default defineComponent({
  data(): state {
    return {
      todos: [
        {id: 0, text: 'текст первой задачи', completed: true},
        {id: 1, text: 'текст третьей задачи', completed: false},
        {id: 2, text: 'текст второй задачи', completed: false}
      ]
    }
  },
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  methods: {
    addTodo(todo: Todo) {
      console.log(todo);
      this.todos.push(todo)
    },
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