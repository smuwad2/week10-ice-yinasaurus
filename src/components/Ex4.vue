<script>
import TaskTracker from './subcomponents/TaskTracker.vue'

export default {
  components: { TaskTracker },
  data() {
    return {
      desc: '',
      deadline: '',
      taskList: []
    }
  },
  methods: {
    add() {
      if (!this.desc || !this.deadline) return

      this.taskList.push({
        desc: this.desc,
        deadline: this.deadline
      })

      this.desc = ''
      this.deadline = ''
    },
    removeTask(idx) {
      this.taskList.splice(idx, 1)
    }
  }
}
</script>

<template>
  <div class="container mt-3">
    <div class="mb-3">
      <label for="desc" class="form-label">Task</label>
      <input type="text" class="form-control" id="desc" v-model="desc" placeholder="task">
    </div>

    <div class="mb-3">
      <label for="deadline" class="form-label">Deadline</label>
      <input type="date" class="form-control" id="deadline" v-model="deadline" placeholder="deadline">
    </div>

    <button type="button" class="btn btn-primary" @click="add">Add New Task</button>
    <hr>

    <!-- Display tasks using TaskTracker -->
    <TaskTracker 
      v-for="(task, index) in taskList"
      :key="index"
      :task="task"
      :idx="index"
      @done="removeTask"
    />
  </div>
</template>
