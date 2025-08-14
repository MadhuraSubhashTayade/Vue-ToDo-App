<script setup>
import { computed, ref } from 'vue';
import TodoList from './TodoList.vue';

const todos = ref([]);
const index = ref(0)
const text = ref('')
const isEdit = ref(false)
const editId = ref(null)

const addToDo = () => {
  if (isEdit.value && editId.value) {
    const todo = todos.value.find(x => x.id === editId.value)
    if (todo) {
      todo.name = text.value
    }
    isEdit.value = false
    editId.value = 0
  } else {
    todos.value.push({ id: ++index.value, name: text.value })
  }
  // reset input box value
  text.value = ''
}

const deleteToDo = (id) => {
  const list = todos.value.filter(x => x.id !== id)
  todos.value = list;
}

const editToDo = (id) => {
  isEdit.value = true
  editId.value = id
  const todo = todos.value.find(x => x.id === id)
  if (todo) text.value = todo.name
}

const btnString = computed(() => {
  return !isEdit.value ? 'Add' : 'Edit'
})

</script>

<template>
  <h1>ToDo List</h1>
  <div class="main-container">
    <div class="top-container">
      <label for="text">Your input:</label>
      <input id="text" type="text" v-model="text" />
      <button :disabled="text == ''" @click="addToDo">{{ btnString }}</button>
    </div>
    <div class="bottom-container">
      <TodoList :todos="todos" @delete-todo="deleteToDo" @edit-todo="editToDo"></TodoList>
    </div>
  </div>
</template>

<style scoped>
* {
  font-size: 24px;
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

h1 {
  text-transform: uppercase;
  letter-spacing: 1.9px;
  font-size: 50px;
  margin: 50px auto;
}

.main-container {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.top-container {
  display: flex;
  gap: 15px;
}

button {
  margin-right: 20px;
  padding: 10px 20px;
  border: none;
  background-color: rgb(25, 118, 210, 0.8);
  color: white;
  border-radius: 4px;
  cursor: pointer;
  font-size: 20px;
  text-transform: uppercase;
}

input {
  padding: 10px;
  outline: none;
  border: none;
  border-bottom: 2px solid green;
  width: 400px;
  position: center;
}

.bottom-container {
  margin-top: 50px;
  min-width: 600px;
}
</style>
