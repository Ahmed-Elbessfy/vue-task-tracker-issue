<template>
  <ul :key="task.id" v-for="task in tasks">
    <Task
      @toggle-reminder="$emit('reminder-toggle', task.id)"
      @task-delete="$emit('delete-task', task.id)"
      :task="task"
    />
  </ul>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "Tasks",
  props: {
    tasks: {
      type: Array,
    },
  },
  components: {
    Task,
  },
  emits: ["delete-task", "reminder-toggle"],
};
</script>

<style scoped>
</style>