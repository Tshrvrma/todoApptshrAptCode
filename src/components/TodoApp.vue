<template>
  <div class="container">
    <!-- Heading -->
    <div class="heading-group dark-theme">
      <h2 class="text-center pt-3 pb-4 text-lg font-bold text-white">My Vue Todo App</h2>
    </div>

    <!-- Input -->
    <div class="input-group pb-4">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="form-control"
      />
      <div class="input-group-append">
        <button class="btn btn-warning" @click="addTask">
          ADD TASK
        </button>
      </div>
    </div>

    <!-- Task list -->
    <div class="list-group">
      <div
        v-for="(task, index) in tasks"
        :key="index"
        class="list-group-item list-group-item-action flex-column align-items-start"
        :class="{'task-completed': task.status === 'finished'}"
      >
        <div class="d-flex w-100 justify-content-between align-items-center">
          <h5 class="mb-1">{{ task.name }}</h5>

          <small>{{ task.date }}</small>
        </div>
        <div class="d-flex w-100 justify-content-between align-items-center">
          <span
            class="badge badge-pill"
            :class="{
              'badge-danger': task.status === 'to-do',
              'badge-warning': task.status === 'in-progress',
              'badge-success': task.status === 'finished',
            }"
            @click="changeStatus(index)"
            style="cursor: pointer;"
          >
            {{ task.status }}
          </span>
          <button
            v-if="task.status !== 'in-progress'"
            class="btn btn-sm btn-primary"
            @click="setInProgress(index)"
          >
            Start
          </button>
          <button class="btn btn-sm btn-danger" @click="deleteTask(index)">
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      task: "",
      tasks: [
        {
          name: "Steal bananas from the supermarket.",
          status: "to-do",
          date: new Date().toLocaleDateString(),
        },
        {
          name: "Eat 1 kg chocolate in 1 hour.",
          status: "in-progress",
          date: new Date().toLocaleDateString(),
        },
        {
          name: "Create YouTube video.",
          status: "finished",
          date: new Date().toLocaleDateString(),
        },
      ],
    };
  },
  methods: {
    changeStatus(index) {
      const task = this.tasks[index];
      if (task.status === "to-do") {
        this.tasks[index].status = "in-progress";
      } else if (task.status === "in-progress") {
        this.tasks[index].status = "finished";
      } else {
        this.tasks[index].status = "to-do";
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    addTask() {
      if (this.task.trim() === "") {
        alert("Please enter a task!");
        return;
      }

      if (this.tasks.some(task => task.name === this.task.trim())) {
        alert("Task with the same name already exists!");
        return;
      }

      this.tasks.push({
        name: this.task.trim(),
        status: "to-do",
        date: new Date().toLocaleDateString(),
      });
      this.task = "";
    },
    setInProgress(index) {
      this.tasks[index].status = "in-progress";
    },
  },
};
</script>

<style scoped>
.dark-theme {
  background-color: #001f3f;
}

.text-white {
  color: #fff; 
  font-style: oblique;
  font-weight: 900;
}

.task-completed {
  background-color: #e6e6e6;
  color: #626a71;
}

.container {
  background-color: #001f3f !important;
  width: 100%;
  height: 100%;
}

.list-group-item {
  margin: 10px;
  border: 4px solid whitesmoke;
}

small {
  color: #001f3f;
}

.btn:hover {
  cursor: pointer;
}
.badge-danger {
  background-color: #dc3545;
}

.badge-warning {
  background-color: #ffc107;
}

.badge-success {
  background-color: #28a745;
}

.badge-pill:hover {
  cursor: pointer;
}
</style>
