<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <button @click="taskStore.deleteTask(task.id)">Delete</button>
            <button @click="taskStore.toggleFav(task.id)">Favorite</button>
        </div>
    </div>
</template>

<script>
import { useTaskStore } from '../stores/TaskStore';

    export default {
        props: ['task'],
        setup() {
            const taskStore = useTaskStore()

            return { taskStore }
        }
    }
</script>

<style>
  .task-list {
    max-width: 640px;
    margin: 20px auto;
  }
  
  .task {
    padding: 6px 20px;
    background: #fff;
    margin-top: 20px;
    border-radius: 4px;
    box-shadow: 2px 4px 6px rgba(0,0,0,0.05);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .task h3,
  .task .icons {
    display: inline-block;
  }

  .task .icons {
    text-align: right;
  }

  .task button {
    padding: 10px 16px;
    font-size: 14px;
    font-weight: bold;
    color: #fff;
    background-color: green;
    border: none;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-left: 8px;
  }

  .task button:hover {
    background-color: #2ecc71;
  }

  .task button:active {
    background-color: #27ae60;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    transform: translateY(1px);
  }
</style>
