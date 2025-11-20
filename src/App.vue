<script setup>
import {computed, onMounted, ref, watch} from "vue";
import Task from "./components/Task.vue";
import AddTask from "./components/AddTask.vue";

onMounted(() => {
  const saved = localStorage.getItem('tasks')
  if (saved) {tasks.value = JSON.parse(saved)}
})

const appName = ref("[Task Manager]")
const tasks = ref([{title: '',task: '',completed:false}])
const newTask = ref([{title:'', task:'', completed:false}])
const addTask = (() =>{
  tasks.value.push({...newTask.value})
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
      newTask.value.title = ''
      newTask.value.task = ''
})
const toggleTask = (i) => {
  tasks.value[i].completed = !tasks.value[i].completed
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}
const toggleFilter = (() =>{
  if (filter.value === 'Completed') {
    filter.value = 'On-Going'
  } else if (filter.value === 'On-Going'){
    filter.value = 'All'
  } else {
    filter.value = 'Completed'
  }
})
const filter = ref('All')
const filterTasks = computed(()=> {
  if (filter.value === 'Completed') {
    return tasks.value.filter(t => t.completed)
  }
  if (filter.value === 'On-Going') {
    return tasks.value.filter(t => !t.completed)
  }
  if (filter.value === 'All'){
    return tasks.value
  }
})
const deleteTask = (i) => {
  tasks.value.splice(i, 1)
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
  }
const showAddTask = ref(false)
const toggleAddTask = () => showAddTask.value = !showAddTask.value
</script>

<template>
  <div class="px-6 bg-blue-900 min-h-screen ">
    <div class="flex justify-between items-center  border-b border-dashed border-slate-300 py-4">
      <h1 class="text-4xl text-white"> {{appName}}</h1>
      <h2  class="text-xl text-white cursor-pointer" @click="toggleFilter">[{{filter}}]</h2>
    </div>
    <Task v-for="(t,i) in filterTasks" :key="i" :task="t" :index="i" :toggleTask="toggleTask" @delete="deleteTask" class="sflex flex-row items-center w-full gap-6" />
    <button @click="toggleAddTask" class="mt-4 text-white text-xl text-left cursor-pointer">[Add Task]</button>
<!--    MODAL-->
    <div v-if="showAddTask" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-blue-900 p-6 border-white border-2 border-dashed shadow-lg w-80 m-2">
        <AddTask :newTask="newTask" :addTask="addTask" :showAddTask="showAddTask" @close="showAddTask = false"/>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
