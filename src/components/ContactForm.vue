<template>
  <div>
    <h1 v-if="!editMode">Add New Contact</h1>
    <h1 v-if="editMode">Edit Contact</h1>
    <form @submit.prevent="submitForm">
      <input v-model="contact.name" placeholder="Name" />
      <input v-model="contact.email" placeholder="Email" />
      <input v-model="contact.phone" placeholder="Phone" />
      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

export default {
  setup() {
    const route = useRoute()
    const router = useRouter()
    const editMode = ref(false)
    const contact = ref({
      id: null,
      name: '',
      email: '',
      phone: ''
    })

    onMounted(() => {
      if (route.params.id) {
        editMode.value = true
        const contacts = JSON.parse(localStorage.getItem('contacts')) || []
        const foundContact = contacts.find(c => c.id === parseInt(route.params.id))
        if (foundContact) {
          contact.value = foundContact
        }
      }
    })

    const submitForm = () => {
      let contacts = JSON.parse(localStorage.getItem('contacts')) || []
      if (editMode.value) {
        const index = contacts.findIndex(c => c.id === contact.value.id)
        contacts[index] = contact.value
      } else {
        contact.value.id = Date.now()
        contacts.push(contact.value)
      }
      localStorage.setItem('contacts', JSON.stringify(contacts))
      router.push('/')
    }

    return { contact, submitForm, editMode }
  }
}
</script>
