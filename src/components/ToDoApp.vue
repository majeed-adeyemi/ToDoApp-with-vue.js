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
        {{ isEditing ? "Update Task" : "Add Task" }}
      </button>
    </div>

    <ul class="list-group">
      <li
        v-for="task in tasks"
        :key="task.id"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <span>{{ task.text }}</span>
        <div>
          <button
            @click="startEditing(task)"
            class="btn btn-sm btn-warning me-2"
          >
            Edit
          </button>
          <button @click="deleteTask(task.id)" class="btn btn-sm btn-danger">
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { db } from "@/firebase";
import {
  collection,
  addDoc,
  getDocs,
  deleteDoc,
  updateDoc,
  doc,
  onSnapshot,
} from "firebase/firestore";

export default {
  data() {
    return {
      tasks: [],
      newTask: "",
      isEditing: false,
      editingId: null,
    };
  },
  async mounted() {
    const tasksRef = collection(db, "tasks");
    // Real-time sync (optional)
    onSnapshot(tasksRef, (snapshot) => {
      this.tasks = snapshot.docs.map((doc) => ({
        id: doc.id,
        ...doc.data(),
      }));
    });
  },
  methods: {
    async addOrUpdateTask() {
      const text = this.newTask.trim();
      if (!text) return;

      if (this.isEditing) {
        const taskRef = doc(db, "tasks", this.editingId);
        await updateDoc(taskRef, { text });
        this.isEditing = false;
        this.editingId = null;
      } else {
        await addDoc(collection(db, "tasks"), { text });
      }

      this.newTask = "";
    },
    startEditing(task) {
      this.newTask = task.text;
      this.isEditing = true;
      this.editingId = task.id;
    },
    async deleteTask(id) {
      await deleteDoc(doc(db, "tasks", id));
      if (this.editingId === id) {
        this.isEditing = false;
        this.editingId = null;
        this.newTask = "";
      }
    },
  },
};
</script>
