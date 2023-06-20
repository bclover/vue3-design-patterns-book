<script lang="ts" setup>
import { computed, ref } from 'vue';

interface ToDo {
  id: number;
  text: string;
  checked: boolean;
}
const _todo_text = ref('');
const _todo_list = ref<ToDo[]>([]);
const _pending = computed(() => {
  return _todo_list.value.filter((todo: ToDo) => !todo.checked);
});
const _done = computed(() => {
  return _todo_list.value.filter((todo: ToDo) => todo.checked);
});
function clearToDo(): void {
  _todo_text.value = '';
}
function addToDo() {
  if (_todo_text.value && _todo_text.value !== '') {
    _todo_list.value.push({
      id: new Date().valueOf(),
      text: _todo_text.value,
      checked: false,
    });
    clearToDo();
  }
}
</script>

<template>
  <div class="todo-container w3-white w3-card-4">
    <!-- Header -->
    <div class="w3-container w3-black w3-margin-0 w3-bottombar w3-border-blue">
      <h1>
        <i class="fa-solid fa-clipboard-list"></i>
        To-Do List
      </h1>
    </div>

    <!-- Remove & Add Buttons -->
    <div
      class="w3-container flex-container w3-light-gray w3-padding-32 w3-center"
    >
      <input
        class="w3-input w3-twothird w3-border"
        type="text"
        autofocus
        v-model="_todo_text"
        @keyup.enter="addToDo()"
        placeholder='Type your "To Do" item here...'
      />
      <button
        class="w3-button w3-gray w3-third"
        style="width: 43px"
        @click="clearToDo()"
      >
        <i class="fa-solid fa-times"></i>
      </button>
      <button class="w3-button w3-blue" @click="addToDo()">
        <i class="fa-solid fa-plus"></i>
        Add To Do
      </button>
    </div>

    <div
      class="w3-container flex-container w3-light-gray w3-padding w3-center"
    ></div>

    <!-- Pending Todos Heading -->
    <div class="w3-padding w3-blue">Pending ({{ _pending.length }})</div>

    <!-- List of Pending Todos -->
    <div class="w3-padding" v-for="todo in _pending" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.checked" />
        <span class="w3-margin-left">
          {{ todo.text }}
        </span>
      </label>
    </div>

    <!-- No Pending Tasks -->
    <div class="w3-padding" v-show="_pending.length == 0">
      No pending tasks.
    </div>

    <!-- Completed Todos Heading -->
    <div class="w3-padding w3-blue">Completed ({{ _done.length }})</div>

    <!-- List of Completed Todos -->
    <div class="w3-padding" v-for="todo in _done" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.checked" />
        <span class="w3-margin-left">
          {{ todo.text }}
        </span>
      </label>
    </div>

    <!-- No Completed Todos -->
    <div class="w3-padding" v-show="_done.length == 0">No completed tasks.</div>
  </div>
</template>

<style scoped>
.todo-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 90vw;
  min-height: 90vh;
  padding: 5rem;
}
</style>
