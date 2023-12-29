<template>
  <footer class="app-footer">
    {{ stats.active }} more to do, {{ stats.done }} done
  </footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export interface Stat {
  active: Number;
  done: Number;
}

export default defineComponent({
  props: {
    stats: {
      type: Object as PropType<Stat>,
    },
  },
});
</script>
