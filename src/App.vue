<template>
    <div class="">
      <h1 class="text-center bg-primary text-white p-3">Vue Todo List</h1>
      <div class="container">
        <div class="row my-5">
          <div class="col">
            <input type="text" class="form-control" v-model="newTask" @keyup.enter="addTask()">
          </div>
          <div class="col">
            <input type="button" value="Add" class="btn btn-secondary" @click="addTask()">
          </div>
        </div>

        <div v-if="filterTask.length > 0">
          <div class="row">
            <div class="col fs-3 mb-4">Tasks</div>
            <div class="col-2 fs-3 mb-4">Done</div>
          </div>

          <div class="row" v-for="(task,key) in filterTask" :key="key">
            <div class="col" :class="task.done ? 'delete' : ''">{{ task.action }}</div>
            <div class="col-2">
              <input type="checkbox" v-model="task.done">
            </div>
          </div>
        </div>
        <div v-else class="alert alert-warning text-center fs-3">There is no data!</div>

        <div class="bg-danger text-center text-white py-2 row mt-3">
          <h5 class="col">Hide Complete Tasks</h5>
          <input type="checkbox" class="col" v-model="hideCompleted">
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    hideCompleted: false,
    newTask: "",
    tasks: [],
  }),
  computed: {
    filterTask() {
      return this.hideCompleted ? this.tasks.filter((v) => !v.done) : this.tasks;
    }
  },
  methods: {
    addTask() {
      if (this.newTask === "") {
        return alert("Please add a task!");
      }
      this.tasks.push({
        action: this.newTask,
        done: false,
      });
      this.newTask = "";
    }
  }
}
</script>

<style>
.delete {
  text-decoration: line-through;
}
</style>