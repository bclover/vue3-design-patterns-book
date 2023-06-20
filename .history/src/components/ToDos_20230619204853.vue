<script lang="ts" setup>
import { computed, ComputedRef, Ref, ref, WritableComputedRef } from 'vue';

interface ToDo {
  id: number;
  text: Ref<string>;
  checked: boolean;
}

const _todo_value = ref('');
const _todo_text: WritableComputedRef<Ref<string>> = computed({
  get: () => _todo_text.value,
  set: (newValue: Ref<string>) => {
    _todo_value.value = newValue.value;
  },
});
const _todo_list = computed(() => []);
const _pending: ComputedRef = computed(() => {
  console.log('pending _todo_list.value ***', _todo_list.value);
  return _todo_list.value.filter((todo) => !todo.checked);
});
const _done: ComputedRef = computed(() => {
  return _todo_list.value.filter((todo) => todo.checked);
});
function clearToDo(): void {
  _todo_text.value = _todo_value;
}
function addToDo() {
  console.log('addToDo =>');
  const date = new Date();
  const todo: ToDo = {
    id: date.valueOf(),
    text: _todo_text.value,
    checked: false,
  };
  console.log('todo =>', todo);
  console.log('_todo_list.value =>', _todo_list.value);
  _todo_list.value.push(todo);
  console.log('_todo_list.value AFTER =>', _todo_list.value);
  clearToDo();
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
    <div class="w3-container flex-container w3-light-gray w3-padding">
      <input
        class="w3-input w3-border-0"
        type="text"
        autofocus
        v-model="_todo_text"
        @keyup.enter="addToDo()"
        placeholder="Type here your to-do item..."
      />
      <button class="w3-button w3-gray" @click="clearToDo()">
        <i class="fa-solid fa-times"></i>
      </button>
      <button class="w3-button w3-blue" @click="addToDo()">
        <i class="fa-solid fa-plus"></i>
      </button>
    </div>

    <!-- Pending Todos Heading -->
    <div class="w3-padding w3-blue">Pending ({{ _pending.length }})</div>

    {{ _pending.length }}

    <!-- List of Pending Todos -->
    <div class="w3-padding" v-for="todo in _pending" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.checked" />
        <span class="w3-margin-left">{{ todo.text }}</span>
      </label>

      <!-- No Pending Tasks -->
      <div class="w3-padding" v-show="_pending.length == 0">No tasks</div>
    </div>

    <!-- Completed Todos Heading -->
    <div class="w3-padding w3-blue">Completed ({{ _done.length }})</div>

    <!-- List of Completed Todos -->
    <div class="w3-padding" v-for="todo in _done" :key="todo.id">
      <label>
        <input type="checkbox" v-model="todo.checked" />
        <span class="w3-margin-left">{{ todo.text }}</span>
      </label>
    </div>

    <!-- No Completed Todos -->
    <div class="w3-padding" v-show="_done.length == 0">No tasks</div>
  </div>
</template>
