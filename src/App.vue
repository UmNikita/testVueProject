<script setup>
import TaskComponent from "./components/TaskComponent.vue"

import { ref, onMounted } from 'vue'

const tasks = ref([])

const getTasks = async () => {
  try {
    const response = await fetch('http://localhost:3004/tasks')
    tasks.value = await response.json()
  } catch (error) {
    console.error('Ошибка загрузке', error)
  }
}

const checkTask = async (taskId) => {
  const task = tasks.value.find(t => t.id === taskId)
  if (!task) return
  try {
    await fetch(`http://localhost:3004/tasks/${taskId}`, {
      method: 'PATCH',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ done: !task.done })
    })
    await getTasks()
    
  } catch (error) {
    console.error('Ошибка при обновлении задачи:', error)
  }
}

onMounted(getTasks)

</script>

<template>
  <div id="container">
    <div id="title">Todo</div>
    <div id="todo-container">
      <div id="todo-wrap">
        <TaskComponent v-for="task in tasks" :key="task.id" :title="task.title" :isDone="task.done" @toggle="() => checkTask(task.id)" />
      </div>
    </div>
  </div>
</template>

<style scoped>
  #title {
    background-color: white;
    height: 50px;
    width: 500px;
    margin-top: 15px;
    color: #2361cc;
    font-size: 45px;
    text-align: center;
  }
  #container {
    height: 100vh;
    background-color: #2361cc;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #todo-container {
    height: 650px;
    width: 750px;
    background-color: white;
    border-radius: 15px;
    margin-top: 75px;
    padding-top: 50px;
    
  }
  #todo-wrap {
    height: 600px;
    overflow: auto;
  }
</style>
