<template>
  <Header :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" title="Task Tracker" />

  <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
  </div>

  <Tasks @toggle-reminder="reminderTask" @delete-task="deleteTask" :tasks="tasks" /> 
</template>

<script>
import Header from './components/Header';
import Tasks from  './components/Tasks';
import AddTask from  './components/AddTask';
 
export default {
  name: 'App' ,
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask(){
       this.showAddTask = !this.showAddTask
    },
    async addTask(task){
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      this.tasks = [...this.tasks, task];
    },
    async deleteTask(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        }) 

        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id != id) : alert('Error deleting task')
      }
    },
    async reminderTask(id) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask)
      })
  
      const data = await res.json();
  
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
    },
    async fetchTasks() {
      const res = await fetch ('api/tasks');

      const data = await res.json();

      return data; 
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);

      const data = await res.json();

      return data; 
    },
  },
  async created() {
    this.tasks = await this.fetchTasks(); 
  }
} 
</script>

<style>
#app {
  padding: 20px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
