<template>
  <div>
    <div class="input-group mb-3">
      <input
        v-model="newTask"
        @keyup.enter="addOrUpdateTask"
        class="form-control"
        placeholder="Enter a task"
      />
      <button @click="addOrUpdateTask" class="btn btn-primary">
        {{ isEditing ? 'Update Task' : 'Add Task' }}
      </button>
    </div>

    <ul class="list-group">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <span>{{ task }}</span>
        <div>
          <button @click="editTask(index)" class="btn btn-sm btn-warning me-2">
            Edit
          </button>
          <button @click="deleteTask(index)" class="btn btn-sm btn-danger">
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
      isEditing: false,
      editingIndex: null
    }
  },
  methods: {
    addOrUpdateTask() {
      const trimmedTask = this.newTask.trim()
      if (!trimmedTask) return

      if (this.isEditing) {
        this.tasks[this.editingIndex] = trimmedTask
        this.isEditing = false
        this.editingIndex = null
      } else {
        this.tasks.push(trimmedTask)
      }
      this.newTask = ''
    },
    editTask(index) {
      this.newTask = this.tasks[index]
      this.isEditing = true
      this.editingIndex = index
    },
    deleteTask(index) {
      this.tasks.splice(index, 1)
      if (this.editingIndex === index) {
        this.newTask = ''
        this.isEditing = false
        this.editingIndex = null
      }
    }
  }
}
</script>
