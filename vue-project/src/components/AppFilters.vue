<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        :class="{ 'button--primary': activeFilter === filter }"
        @click="setFilters(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import type { Filter } from "@/types/filters";

interface State {
  filters: Filter[];
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true,
    },
  },
  data() {
    return {
      filters: ["All", "Active", "Done"],
    };
  },
  methods: {
    setFilters(filter: Filter) {
      this.$emit("setFilter", filter);
    },
  },
  emits: {
    setFilter: (filter: Filter) => filter,
  },
});
</script>
@/types/Filters
