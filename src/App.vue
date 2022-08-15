<script setup lang="ts">
import { ref, reactive, computed } from "vue";
import TodoList from "./components/TodoList.vue";

const placeholder = ref("Название задачи");
const name = ref("");

const todos = reactive([
  {
    name: "Развернуть окружение в Codepen",
    finish: false,
  },
  {
    name: "Пройти курс по Vue",
    finish: false,
  },
  {
    name: "Сделать интернет-магазин на Vue",
    finish: false,
  },
  {
    name: "Пройти HTML",
    finish: true,
  },
  {
    name: "Пройти CSS",
    finish: true,
  },
  {
    name: "Пройти JS",
    finish: true,
  },
]);

const addTodo = () => {
  if (name.value) {
    todos.push({ name: name.value, finish: false });
    name.value = "";
  }
};

const openTasks = computed(() => todos.filter((item) => !item.finish));
const completedTasks = computed(() => todos.filter((item) => item.finish));
const openTasksCount = computed(() => openTasks.value.length);
</script>

<template>
  <div id="app">
    <h1>Список задач</h1>
    <div v-if="openTasksCount > 1">
      Осталось сделать задач: {{ openTasksCount }}
    </div>
    <div v-else-if="openTasksCount > 0">Последний рывок!</div>
    <div v-else>Вы закончили все задачи!</div>
    <Transition>
      <img
        v-show="openTasksCount == 0"
        src="https://st.depositphotos.com/1324256/2282/i/450/depositphotos_22829288-stock-photo-winner-silhouette-on-a-mount.jpg"
        width="150"
        height="150"
      />
    </Transition>
    <TodoList v-if="openTasksCount !== 0" :list="openTasks" />
    <form class="form" @submit.prevent="addTodo">
      <input v-model="name" :placeholder="placeholder" />
      <button type="submit" :disabled="name.length === 0">Добавить</button>
    </form>
    <TodoList title="Завершенные задачи:" :list="completedTasks" />
  </div>
</template>

<style scoped>
.form {
  margin: 20px 0;
}
.v-enter-active,
.v-leave-active {
  transition-property: height, width, transform;
  transition-duration: 0.5s;
  transition-timing-function: ease;
}
.v-enter-from,
.v-leave-to {
  height: 0;
  width: 0;
  transform: rotate(180deg);
}
</style>
