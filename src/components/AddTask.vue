<script setup>
const props = defineProps(['newTask','addTask','showAddTask'])
const emit = defineEmits(['close'])

</script>

<template>
  <div v-if="showAddTask">
    <form class="flex flex-col gap-1 " @submit.prevent="props.addTask">
      <div class="flex flex-col gap-3 mt-1">
        <h2 class="text-white text-xl text-center cursor-pointer">[New Task]</h2>
        <input type="text" v-model="props.newTask.title" placeholder=" Title?" class="bg-blue-900 border border-white text-white">
        <textarea v-model="props.newTask.task" placeholder=" Task?" class="bg-blue-900 border border-white text-white min-h-20"></textarea>
      </div>
      <div class="flex justify-between">
        <button type="submit" class="mt-4 text-white text-xl text-left cursor-pointer">[Complete]</button>
        <button type="button" class="mt-4 text-white text-xl text-left cursor-pointer" @click="emit('close')">[Close]</button>
      </div>
    </form>
  </div>
</template>

<style scoped>

</style>