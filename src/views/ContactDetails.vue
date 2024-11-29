<template>
  <div class="container mt-5">
    <!-- Contact Details Card -->
    <div class="card shadow-lg">
      <div class="card-body">
        <h2 class="card-title text-primary">{{ contact.firstName }} {{ contact.lastName }}</h2>
        <hr />
        <p class="card-text">
          <strong>Email:</strong> {{ contact.email }}
        </p>
        <p class="card-text">
          <strong>Phone:</strong> {{ contact.phone }}
        </p>
      </div>
      <div class="card-footer d-flex justify-content-between">
        <router-link :to="`/edit/${contact.id}`" class="btn btn-warning">
          Edit Contact
        </router-link>
        <button @click="deleteContact" class="btn btn-danger">
          Delete Contact
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    const id = this.$route.params.id;
    const contacts = JSON.parse(localStorage.getItem("contacts")) || [];
    return { contact: contacts.find((c) => c.id === id) };
  },
  methods: {
    deleteContact() {
      const contacts = JSON.parse(localStorage.getItem("contacts")) || [];
      const index = contacts.findIndex((c) => c.id === this.contact.id);
      if (index !== -1) {
        contacts.splice(index, 1);
        localStorage.setItem("contacts", JSON.stringify(contacts));
        this.$router.push("/");
      }
    },
  },
};
</script>

<style scoped>
/* Add spacing between elements */
.card {
  margin-top: 20px;
  border-radius: 8px;
}

.card-title {
  font-size: 2rem;
}

.card-text {
  font-size: 1.2rem;
  margin-bottom: 10px;
}

.card-footer button,
.card-footer a {
  width: 48%;
}
</style>
