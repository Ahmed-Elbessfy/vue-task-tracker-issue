<template>
  <li
    :class="[task.reminder ? 'reminder' : '']"
    @dblclick="$emit('toggle-reminder', task.id)"
  >
    <h3>
      {{ task.txt }}
      <i
        @click="deleteTask(task.id)"
        class="fa fa-times"
        aria-hidden="true"
      ></i>
    </h3>
    <p>{{ task.day }}</p>
  </li>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: {
      type: Object,
    },
  },
  methods: {
    deleteTask(id) {
      this.$emit("task-delete", id);
    },
  },
};
</script>

<style scoped>
li {
  list-style: none;
  background: #f4f4f4;
  margin: 0.5rem;
  padding: 0.8rem 1.4rem;
  cursor: pointer;
  border-left: 5px solid #f4f4f4;
}

li.reminder {
  border-left: 5px solid rgb(5, 157, 5);
}
li h3 {
  text-transform: capitalize;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
li i {
  color: rgb(179, 0, 0);
}
</style>