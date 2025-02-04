
<template>
    <main>

        <!-- heading -->
        <header>
            <img src="./assets/RM.webp" alt="pinia logo">
            <h1>JSE ROAD MAP</h1>
        </header>

        <!-- new task form -->
        <div class="new-task-form">
            <TaskForm></TaskForm>
        </div>

        <!-- filter -->
         <nav class="filter">
            <button @click="filter = 'all'">All Tasks</button>
            <button @click="filter = 'favs'">Completed Tasks</button>
            <button @click="filter = 'UNfavs'">UN-Completed Tasks</button>
         </nav>

         <!-- loading -->
          <div class="loading" v-if="taskStore.loading">Loading...</div>

        <!-- task list -->
         <div class="task-list" v-if="filter === 'all'">
            <p>You have {{ totalCount }} all tasks</p>
            <div v-for="task in tasks" :key="task.id">
                <TaskDetails :task="task"></TaskDetails>
            </div>
         </div>
         <div class="task-list" v-if="filter === 'favs'">
            <p>You have {{ favCount }} completed tasks</p>
            <div v-for="task in favs" :key="task.id">
                <TaskDetails :task="task"></TaskDetails>
            </div>
         </div>
         <div class="task-list" v-if="filter === 'UNfavs'">
            <p>You have {{ UNfavCount }} un-completed tasks</p>
            <div v-for="task in UNfavs" :key="task.id">
                <TaskDetails :task="task"></TaskDetails>
            </div>
         </div>

         <button @click="taskStore.$reset">reset state</button>

    </main>
</template>

<script>
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import { useTaskStore } from './stores/TaskStores';
import { storeToRefs } from 'pinia';
    export default {
  components: {
    TaskForm, TaskDetails },

    setup() {  
        const taskStore = useTaskStore();

        const { tasks, loading, favs, totalCount, favCount, UNfavCount, UNfavs } = storeToRefs(taskStore)

        //fetch tasks
        taskStore.getTasks()

        const filter = ref ('all');


        return { taskStore , filter , tasks, loading, favs, totalCount, favCount, UNfavs, UNfavCount }
    }
}
</script>