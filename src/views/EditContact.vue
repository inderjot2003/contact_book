<template>
  <div class="container mt-5">
    <div class="card shadow">
      <div class="card-header bg-primary text-white">
        <h2 class="text-center mb-0">Edit Contact</h2>
      </div>
      <div class="card-body">
        <form @submit.prevent="updateContact">
          <!-- First Name -->
          <div class="mb-3">
            <label for="firstName" class="form-label">First Name</label>
            <input
              v-model="firstName"
              id="firstName"
              type="text"
              class="form-control"
              placeholder="Enter First Name"
              required
            />
          </div>

          <!-- Last Name -->
          <div class="mb-3">
            <label for="lastName" class="form-label">Last Name</label>
            <input
              v-model="lastName"
              id="lastName"
              type="text"
              class="form-control"
              placeholder="Enter Last Name"
              required
            />
          </div>

          <!-- Email -->
          <div class="mb-3">
            <label for="email" class="form-label">Email</label>
            <input
              v-model="email"
              id="email"
              type="email"
              class="form-control"
              placeholder="Enter Email"
              required
            />
          </div>

          <!-- Phone -->
          <div class="mb-3">
            <label for="phone" class="form-label">Phone</label>
            <input
              v-model="phone"
              id="phone"
              type="tel"
              class="form-control"
              placeholder="Enter Phone Number"
            />
          </div>

          <!-- Submit Button -->
          <div class="text-center">
            <button type="submit" class="btn btn-success px-5">Update Contact</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    const id = this.$route.params.id;
    const contacts = JSON.parse(localStorage.getItem("contacts")) || [];
    const contact = contacts.find((c) => c.id === id);
    return { ...contact };
  },
  methods: {
    updateContact() {
      const contacts = JSON.parse(localStorage.getItem("contacts")) || [];
      const index = contacts.findIndex((c) => c.id === this.$route.params.id);
      if (index !== -1) {
        contacts[index] = {
          ...contacts[index],
          firstName: this.firstName,
          lastName: this.lastName,
          email: this.email,
          phone: this.phone,
        };
        localStorage.setItem("contacts", JSON.stringify(contacts));
        this.$router.push(`/contact/${this.$route.params.id}`);
      }
    },
  },
};
</script>

<style scoped>
/* Styling the card for responsiveness */
.card {
  max-width: 600px;
  margin: 0 auto;
  border-radius: 15px;
}

.card-header {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}

button {
  font-size: 1.2rem;
}
</style>
