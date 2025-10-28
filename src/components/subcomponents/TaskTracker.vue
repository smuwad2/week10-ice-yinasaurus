<script>
export default {
  props: {
    task: Object,
    idx: Number
  },
  methods: {
    markDone() {
      this.$emit('done', this.idx)
    }
  }
}
</script>

<template>
  <div class="card mb-2">
    <div class="card-body d-flex justify-content-between align-items-center">
      <div>
        <h5 class="card-title">Deadline: {{ task.deadline }}</h5>
        <p class="card-text">{{task.desc}}</p>
      </div>
      <button class="btn btn-success" @click="markDone">Done</button>
    </div>
  </div>
</template>
