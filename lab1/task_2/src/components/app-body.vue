<template>
  <div class="body">
    <div class="d-flex justify-content-between align-items-center mb-4">
      <h4 class="mb-0">Student Management</h4>
      <button class="btn btn-primary" @click="showModal = true">
        <i class="bi bi-plus-circle me-1"></i> Add Student
      </button>
    </div>

    <div class="card shadow-sm">
      <div class="card-body">
        <div v-if="students.length == 0" class="text-center py-5">
          <i class="bi bi-people fs-1 text-muted"></i>
          <h4 class="mt-3 text-muted">No students yet</h4>
          <p class="text-muted">Click "Add Student" to get started</p>
        </div>
        <div v-else class="table-responsive">
          <table class="table table-hover">
            <thead class="table-light">
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Name</th>
                <th scope="col">City</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="row in students" :key="row.id">
                <th scope="row" class="text-muted">{{ row.id }}</th>
                <td>{{ row.name }}</td>
                <td>{{ row.city }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <div
      v-if="showModal"
      class="modal-backdrop fade show"
      @click="cancelModal()"
    ></div>

    <div v-if="showModal" class="modal d-block" tabindex="-1">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content shadow">
          <div class="modal-header bg-light">
            <h5 class="modal-title">Add New Student</h5>
            <button
              type="button"
              class="btn-close"
              aria-label="Close"
              @click="cancelModal()"
            ></button>
          </div>
          <form @submit.prevent="addNewStudent(formData.name, formData.city)">
            <div class="modal-body">
              <div class="mb-3">
                <label for="studentName" class="form-label">Name</label>
                <input
                  v-model="formData.name"
                  type="text"
                  class="form-control"
                  id="studentName"
                  placeholder="Enter student name"
                />
              </div>
              <div class="mb-3">
                <label for="studentCity" class="form-label">City</label>
                <input
                  v-model="formData.city"
                  type="text"
                  class="form-control"
                  id="studentCity"
                  placeholder="Enter student city"
                />
              </div>
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                @click="cancelModal()"
              >
                Cancel
              </button>
              <button type="submit" class="btn btn-primary">
                Save Student
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    students: [],
    showModal: false,
    formData: {
      name: "",
      city: "",
    },
  }),

  methods: {
    addNewStudent(rawName, rawCity) {
      const name = rawName?.trim();
      const city = rawCity?.trim();
      if (!name || !city) {
        alert("Please fill all fields");
        return;
      }
      this.students.push({
        name,
        city,
        id: Math.random().toString(36).slice(3, 6),
      });
      this.cancelModal();
    },
    cancelModal() {
      this.formData = {
        name: "",
        city: "",
      };
      this.showModal = false;
    },
  },
};
</script>

<style scoped>
.body {
  grid-column: 2 / -1;
  padding: 1rem;
}
</style>
