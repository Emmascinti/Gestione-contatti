<template>
  <div>
    <AppHeader @updateSearch="updateSearch" />
    <ContactList
      :contacts="filteredContacts"
      @removeContact="removeContact"
      @updateContact="updateContact"
    />
    <AddContactForm @addContact="addContact" />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import ContactList from "./components/ContactList.vue";
import AddContactForm from "./components/AddContactForm.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    ContactList,
    AddContactForm,
  },
  data() {
    return {
      contacts: [], // Lista dei contatti
      searchQuery: "", // Query di ricerca
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts.filter((contact) =>
        contact.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    updateSearch(query) {
      this.searchQuery = query;
    },
    addContact(newContact) {
      this.contacts.push(newContact);
      this.saveContacts();
    },
    removeContact(index) {
      this.contacts.splice(index, 1);
      this.saveContacts();
    },
    updateContact({ index, updatedContact }) {
      this.contacts.splice(index, 1, updatedContact); 
      this.saveContacts();
    },
    saveContacts() {
      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    },
  },
  created() {
    const savedContacts = localStorage.getItem("contacts");
    if (savedContacts) {
      this.contacts = JSON.parse(savedContacts);
    }
  },
};
</script>
