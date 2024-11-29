<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <!-- Form Card -->
      <div class="col-md-6">
        <div class="card shadow-lg">
          <div class="card-header bg-primary text-white text-center">
            <h2>Add New Contact</h2>
          </div>
          <div class="card-body">
            <form @submit.prevent="addContact">
              <!-- First Name -->
              <div class="form-group mb-3">
                <label for="firstName" class="form-label">First Name</label>
                <input
                  type="text"
                  id="firstName"
                  v-model="firstName"
                  class="form-control"
                  placeholder="Enter first name"
                  required
                />
              </div>
              <!-- Last Name -->
              <div class="form-group mb-3">
                <label for="lastName" class="form-label">Last Name</label>
                <input
                  type="text"
                  id="lastName"
                  v-model="lastName"
                  class="form-control"
                  placeholder="Enter last name"
                  required
                />
              </div>
              <!-- Email -->
              <div class="form-group mb-3">
                <label for="email" class="form-label">Email</label>
                <input
                  type="email"
                  id="email"
                  v-model="email"
                  class="form-control"
                  placeholder="Enter email address"
                  required
                />
              </div>
              <!-- Phone -->
              <div class="form-group mb-4">
                <label for="phone" class="form-label">Phone</label>
                <input
                  type="text"
                  id="phone"
                  v-model="phone"
                  class="form-control"
                  placeholder="Enter phone number (optional)"
                />
              </div>
              <!-- Submit Button -->
              <div class="d-grid">
                <button type="submit" class="btn btn-primary">
                  Add Contact
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      phone: "",
    };
  },
  methods: {
    addContact() {
      const newContact = {
        id: Date.now().toString(),
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        phone: this.phone,
      };
      const contacts = JSON.parse(localStorage.getItem("contacts")) || [];
      contacts.push(newContact);
      localStorage.setItem("contacts", JSON.stringify(contacts));
      this.$router.push(`/contact/${newContact.id}`);
    },
  },
};
</script>

<style scoped>
.card {
  border-radius: 12px;
}

.card-header {
  font-size: 1.5rem;
  font-weight: 600;
}

.form-label {
  font-weight: 500;
  font-size: 1rem;
}

button {
  font-size: 1.2rem;
  padding: 10px;
}

.container {
  padding-top: 20px;
  padding-bottom: 40px;
}
</style>
