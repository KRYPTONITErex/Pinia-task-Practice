<template>
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">

        <i class="material-icons"
          @click="taskStore.deleteTask(task.id)"
        > delete </i>
        <i class="material-icons"
          :class="{ active: task.isFav }"
          @click="taskStore.togglefav(task.id)"
        > assignment_turned_in </i>

    </div>
  </div>
</template>

<script>
import { useTaskStore } from '@/stores/TaskStores';

export default {
    props: ['task'],
    setup() {
      const taskStore = useTaskStore();

      return { taskStore }
    }

}
</script>

<style>


</style>