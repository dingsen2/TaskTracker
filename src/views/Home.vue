<template>
  <div v-show="showBtn">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'
export default {
    name:'Home',
    props: {
        showBtn: Boolean
    },
    components: {
        Tasks,
        AddTask
    },
    data() {
        return {
            tasks: [],
        }
        
    },
      methods: {
    async deleteTask(id){
      if(confirm('Are your sure')){
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status == 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('error deleting things')
      }
    },

    async toggleReminder(id){
      const taskToToggle = await this.fetchTask(id)
      const updateTask = {...taskToToggle, reminder:!taskToToggle.reminder}
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updateTask)
      })

      const data = await res.json()
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
    },

    async addTask(task){
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },

    async fetchTasks(){
      const res = await fetch('api/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()
      return data
    }
  },

  async created() {
    this.tasks = await this.fetchTasks()
  }
}
</script>

