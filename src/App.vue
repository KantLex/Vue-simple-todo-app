<template>
  <div id="app">
    <h1>Simple To-Do List</h1>

    <div class="add-task">
      <input v-model="newTask" type="text" placeholder="Add a new task" />
      <button @click="addTask">Add Task</button>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="toggleTaskCompletion(index)">
          {{ task.completed ? "Undo" : "Complete" }}
        </button>
        <button @click="removeTask(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "", // To hold the value of new task input
      tasks: [] // To hold the list of tasks
    };
  },
  methods: {
    addTask() {
      // Ensure that the input is not empty
      if (this.newTask.trim() !== "") {
        // Add new task to the tasks array
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = ""; // Reset the input field
      }
    },
    toggleTaskCompletion(index) {
      // Toggle the completion status of the task
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    removeTask(index) {
      // Remove the task from the array
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}

h1 {
  font-size: 2rem;
  margin-bottom: 20px;
}

.add-task {
  margin-bottom: 20px;
}

.add-task input {
  padding: 10px;
  font-size: 1rem;
  width: 250px;
}

.add-task button {
  padding: 10px 15px;
  margin-left: 10px;
  font-size: 1rem;
  cursor: pointer;
}

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-item {
  margin-bottom: 10px;
}

.task-item span {
  font-size: 1.2rem;
  margin-right: 20px;
}

.task-item button {
  margin-left: 10px;
  padding: 5px 10px;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: gray;
}
</style>