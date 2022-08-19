<script setup lang="ts">
const props = defineProps<{ count: number }>();
const emit = defineEmits<{
  (event: "increment", count: number): void;
}>();

const increment = () => emit("increment", props.count + 1);
</script>

<template>
  <button type="button" @click="increment">
    <slot></slot>
    {{ props.count }}
  </button>
</template>

<style scoped></style>
