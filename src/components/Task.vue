<script setup>
const props = defineProps(['task','toggleTask', "index"])
const emit = defineEmits(['delete', 'edit'])
</script>

<template>
  <!--    TASKS-->
 <div class="flex items-center gap-4 border-b border-dashed border-slate-300 mt-1 ml-4">
   <h3 class="text-white text-lg">{{index + 1}} >> </h3>
   <!--title, task-->
   <div class="flex flex-col flex-1">
     <h2 class="text-white text-lg"> {{task.title}} </h2>
     <h3 class="ml-4 text-slate-300 text-sm"> {{task.task}} </h3>
   </div>

   <!--completed-->
   <div class="flex flex-col items-center">
     <h3 class="text-slate-300 text-sm" ></h3>
     <div class="flex items-center justify-center gap-2">
       <h2 class="text-white text-lg cursor-pointer" @click="toggleTask(index)">{{task.completed? '[Completed]':'[On-Going]'}}</h2>
       <button class="text-white text-lg cursor-pointer hover:text-red-500" @click="emit('delete', index)">[x]</button>
     </div>
   </div>
 </div>

</template>

<style scoped>

</style>