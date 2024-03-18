<template>
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">
      <i class="material-icons" @click="taskStore.deleteTask(task.id)">delete</i>
      <i class="material-icons" :class="{'fav' : task.isFav}" @click="taskStore.toggleFav(task.id)">favorite</i>
    </div>
  </div>
</template>

<script setup>
import { useTaskStore } from '@/stores/TaskStore';
  const taskStore =useTaskStore()
  const props = defineProps(['task'])

</script>
<style scoped>
  .task{
    display: flex;
    padding: 15px;
    border-bottom: 3px solid #000;
    justify-content: space-between;
    align-items: center;
  }
  .icons{
    display: flex;
    gap: 10px;
  }
  i{
    cursor: pointer;
    color: #bbb;
  }
  .fav{
    color: red;
  }
</style>