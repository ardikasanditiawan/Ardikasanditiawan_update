<template>
  <main>
    <header class="header">
      <img class="logo" src="../assets/LogoPinia.png" alt="PiniaLogo">
      <h1 class="name">Store Ilham</h1>
    </header>

    <!-- task -->
    <div class="new-task-form">
      <TaskForm />
    </div>

      <!--Filter-->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!--loading-->
    <div class="loading" v-if="loading">Loading Tasks...</div>

    <!-- task-list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>Your have {{ totalCount }} task left to do</p>
        <div v-for="task in tasks">
          <TaskDetails :task="task" /> 
        </div>
      </div>
     <div class="task-list" v-if="filter === 'favs'">
      <p>Your have {{ favCount }} favs left to do</p>
        <div v-for="task in favs">
          <TaskDetails :task="task" /> 
        </div>
      </div>

      <div class="reset"><button @click="taskStore.$reset">Reset State</button></div>
      

  </main>
</template>

<script>
  import TaskDetails from '../components/TaskDetail.vue'
  import TaskForm from '../components/TaskForm.vue'
  import { ref } from 'vue'
  import { useTaskStore } from '../stores/TaskStore'
import { storeToRefs } from 'pinia'

  export default {
    components: { TaskDetails, TaskForm },
    setup () {
      const taskStore = useTaskStore()

      const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

      // fetch task
      taskStore.getTasks()

      const filter = ref('all')

      return { taskStore, filter, tasks, loading, favs, totalCount, favCount }
    }
  }
</script>

<style>
  .header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1px;
    background-color: #f2f2f2;
  }

  .logo {
    width: 60px;
    height: 80px;
    margin-right: 10px;
  }

  .name {
    font-size: 24px;
    font-weight: bold;
    display: flex;
    align-items: center;
  }

  .loading {
    max-width: 640px;
    border: 1px solid #ffd859;
    background: #ffe9a0;
    color: #3a3a3a;
    padding: 5px 0;
    text-align: center;
    margin: 30px auto;
  }

  .filter {
  margin: 10px 0;
}

.filter button {
  margin-right: 10px;
  background-color: green;
  color: white;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.reset button {
  padding: 16px;
  font-size: 14px;
  font-weight: bold;
  color: #fff;
  background-color: green;
  border: none;
  border-radius: 25px;
  cursor: pointer;
}

</style>
