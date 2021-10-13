<template>
  <header>
    <h1>
      {{ title }}
    </h1>
    <Button
      @btn-click="$emit('toggle-form-show')"
      :txt="showAddTask ? 'close' : 'add task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Task Tracker",
    },
    showAddTask: {
      type: Boolean,
      default: false,
    },
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  text-transform: capitalize;
}
</style>