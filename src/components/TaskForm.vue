<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="newTask" type="text" placeholder="Нужно сделать...." />
    <button type="submit">Добавить</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useTaskStore } from '../stores/TaskStore'
const taskStore = useTaskStore();
const newTask = ref('');
const handleSubmit = () => {
  if (newTask.value.length > 0) {
    taskStore.addTask({
      title: newTask.value,
      isFav: false,
      id: Math.floor(Math.random() * 10000)
    })
    newTask.value = ''
  }
}
</script>

<style scoped>
form {
  display: flex;
  gap: 15px;
  width: 100%;
  padding: 15px 30px;
}

input {
  width: 100%;
  padding: 15px 10px;
  border: none;
  background: none;
  color: #fff;
  border-bottom: 3px solid #fff;
}
::placeholder{
  color: #fff;
  font-size: 18px;
}
button{
  cursor: pointer;
  padding: 10px 20px;
  border-style: none;
  border-radius: 10px;
  background: none;
  border: 1px solid #fff;
  font-size: 18px;
  color: #fff;
}
</style>