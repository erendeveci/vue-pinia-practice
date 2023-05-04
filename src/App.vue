<template>
  <main>
    <!-- heading-->
    <header>
      <img src="./assets/logo.svg" alt="logo" />
      <h1>Pinia Tasks</h1>
    </header>

  <!-- form -->
  <div class="new-task-form">
    <task-form></task-form>
  </div>
  
  
    <!-- filter-->

    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'favs'">Favorite Tasks</button>
    </nav>
    <!--task-->

    <div class="task-list" v-if="filter === 'all'">
      <p>
        Your have <span>{{ taskStore.totalCount }}</span> task left to do...
      </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <task-details :task="task"></task-details>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>
        Your have <span> {{ taskStore.favCount }} </span>favorite left to do...
      </p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <task-details :task="task"></task-details>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue";
import { useTaskStore } from "./stores/TaskStore.js";
import TaskForm from './components/TaskForm.vue';
export default {
  setup() {
    const taskStore = useTaskStore();

    const filter = ref("all");

    return { taskStore, filter };
    //it's available(task-store) inside our view template now
  },
  components: {
    TaskDetails,
    TaskForm,
  },
  methods : {

  }
};
</script>
