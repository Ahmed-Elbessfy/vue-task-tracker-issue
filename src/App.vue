<template>
  <div class="container">
    بسم الله الرحمن الرحيم و الصلاة و السلام على مولانا سيد الخلق أجمعين
    <Header
      title="task tracker"
      :showAddTask="showAddTask"
      @toggle-form-show="toggleFormShow"
    />
    <AddTasks v-show="showAddTask" @add-task="addTask" />
    <Tasks
      @delete-task="deleteTask"
      @reminder-toggle="toggleReminder"
      :tasks="tasks"
    />
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";
import Tasks from "./components/Tasks";
import AddTasks from "./components/AddTasks";
export default {
  name: "App",
  components: {
    Header,
    Footer,
    Tasks,
    AddTasks,
  },
  data() {
    return {
      tasks: [],
      showAddTask: true,
    };
  },
  methods: {
    async deleteTask(id) {
      const deleteCall = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });

      deleteCall.status === 200
        ? (this.tasks = this.tasks.filter((t) => t.id !== id))
        : alert("Error Deleteing task");
    },
    async toggleReminder(id) {
      // udpate database
      const taskToToggle = await this.fetchTask(id);

      let updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });
      const fetchUdpTask = await res.json();

      // update UI
      this.tasks.forEach((task) => {
        if (task.id === id) {
          task.reminder = fetchUdpTask.reminder;
        }
      });
    },
    async addTask(task) {
      // update Database
      const call = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const newTask = await call.json();

      // update UI
      this.tasks = [...this.tasks, newTask];
    },
    toggleFormShow() {
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks() {
      const data = await fetch("api/tasks");
      const result = await data.json();

      return result;
    },
    async fetchTask(id) {
      const data = await fetch(`api/tasks/${id}`);
      const result = await data.json();

      return result;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Poppins", Helvetica, Arial, sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  text-transform: capitalize;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
