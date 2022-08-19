<script setup lang="ts">
import ButtonCount from "../components/ButtonCount.vue";

const props = defineProps<{
  list: {
    finish: boolean;
    name: string;
    likes: number;
    dislikes: number;
  }[];
  title?: string;
}>();
</script>

<template>
  <h2 v-if="props.title?.length || 0 > 0">{{ props.title }}</h2>
  <ul class="list">
    <TransitionGroup>
      <li
        v-for="todo in props.list"
        class="item"
        :class="{ done: todo.finish }"
        :key="todo.name"
      >
        <input v-model="todo.finish" type="checkbox" />
        {{ todo.name }}
        <ButtonCount :count="todo.likes" @increment="todo.likes++"
          >Лайк</ButtonCount
        >
        <ButtonCount :count="todo.dislikes" @increment="todo.dislikes++"
          >Дизлайк</ButtonCount
        >
      </li>
    </TransitionGroup>
  </ul>
</template>

<style scoped>
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
}
.item {
  margin: 10px 0;
}
.done {
  text-decoration: line-through;
}
.v-enter-active,
.v-leave-active {
  transition-property: opacity;
  transition-duration: 0.5s;
  transition-timing-function: ease;
}
.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
