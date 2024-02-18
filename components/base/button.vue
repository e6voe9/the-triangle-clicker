<script setup lang="ts">
interface Props {
  text: string;
}

const props = defineProps<Props>();
</script>

<template>
  <button
    type="button"
    class="px-2 font-mono text-sm font-bold border border-gray-700 rounded-full bg-slate-200"
  >
    {{ text }}
  </button>
</template>
