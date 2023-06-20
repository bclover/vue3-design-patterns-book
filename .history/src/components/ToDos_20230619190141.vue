<script setup lang="ts">
import { ref, computed, ComputedRef } from 'vue'; //1
const _todo_text = ref('');
const _todo_list = ref([]);
const _pending: ComputedRef<never[]> = computed(() => {
  return _todo_list.value.filter((item = !item.checked));
});
const _done: ComputedRef<never[]> = computed(() => {
  return _todo_list.value.filter((item) => item.checked);
});
function clearToDo(): void {
  _todo_text.value = '';
}
function addToDo() {
  //6
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

<div class="todo-container w3-white w3-card-4">                    //1
  <!-- Simple header -->                                         //2
  <div class="w3-container w3-black w3-margin-0
      w3-bottombar w3-border-blue">
      <h1>
          <i class="fa-solid fa-clipboard-list"></i>
          To-Do List
      </h1>
</div>
