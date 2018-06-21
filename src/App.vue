<template>
  <div class="wrapper">

    <div class="container">

      <Header :totalTasks="this.tasks.length" />

      <Form @addTask="addTask" />

      <Tasks>
        <Task
          @doneTask="doneTask"
          @removeTask="removeTask"
          v-for="task in tasks"
          :key="task.id"
          :task="task"
        />
      </Tasks>
    </div>

  </div>
</template>

<script>
import Header from './components/Header';
import Form from './components/Form';
import Tasks from './components/Tasks';
import Task from './components/Task';

export default {
  components: {
    Header,
    Form,
    Tasks,
    Task,
  },

  data() {
    return {
      tasks: [],
    }
  },

  mounted() {
    this.getTasksFromStorage();
  },

  methods: {
    addTask(name) {
      const newTask = { id: this.tasks.length + 1, name: name, done: false };

      this.tasks = [... this.tasks, newTask];
    },

    doneTask(task_id) {
      this.tasks = this.tasks.map(task => {
        if(task.id === task_id)
          task.done = !task.done;

        return task;
      });
    },

    removeTask(task_id) {
      this.tasks = this.tasks.filter(task => task.id !== task_id);
    },

    getTasksFromStorage() {
      if(!'localStorage' in window) {
        return;
      }

      this.tasks = JSON.parse(window.localStorage.getItem('tasks'));
    },

    saveToStorage() {
      if(!'localStorage' in window) {
        return;
      }

      window.localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
  },

  watch: {
    'tasks'() {
      this.saveToStorage();
    },
  },
}
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
    outline: none;
  }

  body {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
    font-size: 16px;
    background-color: #cccccc;
  }

  .wrapper {
    display: flex;
    justify-content: center;
    padding: 1.5rem;

    .container {
      width: 100%;

      @media screen and (min-width: 768px) {
        max-width: 50vw;
      }
    }
  }
</style>
