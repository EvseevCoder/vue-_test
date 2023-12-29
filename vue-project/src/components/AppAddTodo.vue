<template>
  <section class="add-todo">
    <form v-if="isformVisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="closeform">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import type { Todo } from "@/types/Todo";
import { defineComponent } from "vue";

interface State {
  isformVisible: boolean;
  todoText: string;
}

export default defineComponent({
  data(): State {
    return {
      isformVisible: false,
      todoText: "",
    };
  },
  methods: {
    showForm() {
      this.isformVisible = true;
    },
    closeform() {
      this.isformVisible = false;
    },
    addTodo() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      });
      (this.todoText = ""), (this.isformVisible = false);
    },
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
});
</script>
