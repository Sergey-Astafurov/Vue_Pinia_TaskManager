<template>
  <header>
    <h1>Pinia Task</h1>

    <section><TaskForm/></section>
  </header>
  <nav class="filter">
    <button @click="filter = 'all'">all Task</button>
    <button @click="filter = 'favs'">favs Task</button>
  </nav>
  <div class="loading" v-if="taskStore.isLoading">
    loading task...
  </div>
  <main>
    <div class="tasks-list" v-if="filter == 'all'">
      <p>У тебя {{ taskStore.totalCount }} задач</p>
      <div class="task" v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="tasks-list"  v-if="filter == 'favs'">
      <p>у тебя {{ taskStore.favCount }} любимых задач</p>
      <div class="task" v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
    <button class="reset" @click="taskStore.$reset">reset state</button>
  </main>
</template>



<script setup>
import TaskForm from './components/TaskForm.vue'
import { RouterLink, RouterView } from "vue-router";
import { useTaskStore } from './stores/TaskStore'
import TaskDetails from './components/TaskDetails.vue'
import {ref} from 'vue'
import { storeToRefs } from 'pinia';
const taskStore = useTaskStore()
const filter = ref('all')
taskStore.getTasks()
const {tasks, loading, favs, totalCount} = storeToRefs(taskStore)
</script>



<style scoped>
header{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px 0;
  background: rgb(90, 219, 166);
  color: #fff;
}
h1 {
  color: #fff;
  font-size: 50px;
}
.tasks-list{
  padding: 30px 0;
  width: 900px;
  margin: 0 auto;
}
.filter{
  width: 900px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
  margin: 10px auto;

}
button{

  cursor: pointer;
  padding: 10px 20px;
  border-style: none;
  border-radius: 10px;
  background: none;
  border: 1px solid #000;
  font-size: 18px;
}
section{
  display: block;
  width: 400px;
  margin: 0 auto;
}
.reset{
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
