<template>
    <div @dblclick="toggle_reminder(task.id)"  :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>
            {{task.text}}
            <em @click="$emit('delete-task', task.id)" class="fas fa-times"></em>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: Object
        },
        methods: {
            toggle_reminder(id) {
                this.$emit('toggle-reminder', id)
            }
        }
    }
</script>

<style scope>
    .fas {
      color: red;
    }
    .task {
      background: #f4f4f4;
      margin: 5px;
      padding: 10px 20px;
      cursor: pointer;
    }
    .task.reminder {
      border-left: 5px solid green;
    }
    .task h3 {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
</style>