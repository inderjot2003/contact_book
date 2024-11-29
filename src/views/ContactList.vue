<template>
  <div class="container mt-5">
    <!-- Search Section -->
    <div class="input-group mb-4">
      <input
        v-model="searchQuery"
        type="text"
        class="form-control"
        placeholder="Search contacts by name"
      />
    </div>

    <!-- Contact List -->
    <ul class="list-group mb-4">
      <li
        v-for="contact in filteredContacts"
        :key="contact.id"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <router-link :to="`/contact/${contact.id}`" class="text-decoration-none">
          {{ contact.firstName }} {{ contact.lastName }}
        </router-link>
      </li>
    </ul>

    <!-- Add New Contact Button -->
    <div class="text-center">
      <router-link to="/add" class="btn btn-primary">Add New Contact</router-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      contacts: JSON.parse(localStorage.getItem("contacts")) || [],
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts
        .filter((contact) =>
          contact.firstName
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase()) ||
          contact.lastName.toLowerCase().includes(this.searchQuery.toLowerCase())
        )
        .sort((a, b) => a.lastName.localeCompare(b.lastName));
    },
  },
};
</script>

<style scoped>
/* Highlight list items on hover */
.list-group-item:hover {
  background-color: #f8f9fa;
  transition: background-color 0.3s ease;
}

/* Center the add button for better design */
.text-center {
  margin-top: 20px;
}
</style>
