<template>
  <form @submit="submitForm" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" name="text" v-model="txt" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        name="day"
        v-model="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",

  data() {
    return {
      txt: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    submitForm(e) {
      e.preventDefault();
      if (this.txt && this.day) {
        this.$emit("add-task", {
          txt: this.txt,
          day: this.day,
          reminder: this.reminder,
        });
      } else {
        alert("please enter valid task and time");
      }
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>