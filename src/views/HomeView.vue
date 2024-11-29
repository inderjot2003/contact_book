<template>
  <div class="container mt-5">
    <!-- Header Section -->
    <div class="d-flex justify-content-between align-items-center mb-4">
      <h2 class="fw-bold">Contact List</h2>
      <button
        class="btn btn-outline-primary rounded-pill px-4 py-2 shadow-sm"
        @click="toggleAddForm"
      >
        <i class="fas" :class="showAddForm ? 'fa-times' : 'fa-plus'"></i>
        {{ showAddForm ? "Cancel" : "Add New Contact" }}
      </button>
    </div>

    <!-- Search Input -->
    <div class="input-group mb-3">
      <input
        v-model="search"
        type="text"
        class="form-control shadow-sm"
        placeholder="🔍 Search contacts by name"
        aria-label="Search contacts"
      />
    </div>

    <!-- Add Contact Form -->
    <ContactForm
      v-if="showAddForm"
      @submit="addContact"
      @cancel="cancelAddForm"
      class="mb-4"
    />

    <!-- Contact List -->
    <ul class="list-group">
      <li
        v-for="contact in filteredContacts"
        :key="contact.id"
        class="list-group-item list-group-item-action d-flex justify-content-between align-items-center border-0 shadow-sm mb-2"
      >
        <router-link
          :to="'/contact/' + contact.id"
          class="text-decoration-none text-dark fw-bold"
        >
          <span>
            <i class="fas fa-user-circle me-2 text-primary"></i>
            {{ contact.firstName }} {{ contact.lastName }}
          </span>
        </router-link>
        <span class="badge bg-primary rounded-pill px-3 py-2">
          <i class="fas fa-envelope me-1"></i> {{ contact.email }}
        </span>
      </li>
    </ul>

    <!-- Empty State -->
    <p v-if="filteredContacts.length === 0" class="text-center mt-4 text-muted">
      <i class="fas fa-info-circle me-2"></i>No contacts found. Try adding one!
    </p>
  </div>
</template>

<script>
import ContactForm from "../components/ContactForm.vue";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      contacts: JSON.parse(localStorage.getItem("contacts")) || [],
      search: "",
      showAddForm: false,
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts
        .filter(
          (contact) =>
            contact.firstName
              .toLowerCase()
              .includes(this.search.toLowerCase()) ||
            contact.lastName.toLowerCase().includes(this.search.toLowerCase())
        )
        .sort((a, b) => a.lastName.localeCompare(b.lastName));
    },
  },
  methods: {
    toggleAddForm() {
      this.showAddForm = !this.showAddForm;
    },
    addContact(newContact) {
      newContact.id = Date.now();
      this.contacts.push(newContact);
      this.saveContacts();
      this.showAddForm = false;
    },
    cancelAddForm() {
      this.showAddForm = false;
    },
    saveContacts() {
      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    },
  },
};
</script>

<style scoped>
/* General Styling */
h2 {
  font-size: 1.75rem;
}

/* Buttons */
.btn {
  font-size: 1rem;
  font-weight: 600;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.btn:hover {
  background-color: #007bff;
  color: #fff;
  box-shadow: 0 4px 10px rgba(0, 123, 255, 0.2);
}

/* List Items */
.list-group-item {
  border-radius: 10px;
  background-color: #f8f9fa;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.list-group-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Empty State */
.text-muted {
  font-style: italic;
  font-size: 1.1rem;
}

/* Responsive Styling */
@media (max-width: 576px) {
  .d-flex {
    flex-direction: column;
    gap: 10px;
  }
  h2 {
    text-align: center;
  }
}
</style>
