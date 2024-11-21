<template>
  <div class="p-4">
    <p v-if="contacts.length === 0" class="text-center text-gray-300 italic">
      Nessun contatto trovato.
    </p>
    <div v-if="isEditing" class="mt-6 bg-gradient-to-r from-gray-800 via-gray-700 to-gray-600 p-6 rounded-xl shadow-xl">
      <h3 class="text-lg font-semibold mb-4 text-white">Modifica Contatto</h3>
      <form @submit.prevent="updateContact" class="space-y-2">
        <input
          type="text"
          v-model="editContactData.name"
          placeholder="Nome"
          class="w-full p-3 border border-gray-500 rounded-lg bg-gray-800 text-gray-300 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-400"
        />
        <input
          type="tel"
          v-model="editContactData.phone"
          placeholder="Numero"
          class="w-full p-3 border border-gray-500 rounded-lg bg-gray-800 text-gray-300 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-400"
        />
        <br>
        <br>
        <div class="flex space-x-2">
          <button
            type="submit"
            class="px-5 py-2 bg-blue-500 text-white font-semibold rounded-lg hover:bg-blue-400 transition-all"
          >
            Salva
          </button>
          <button
            type="button"
            @click="cancelEdit"
            class="px-5 py-2 bg-gray-600 text-white font-semibold rounded-lg hover:bg-gray-500 transition-all"
          >
            Annulla
          </button>
        </div>
      </form>
    </div>
    <br>

    <ol class="space-y-4">
      <li
        v-for="(contact, index) in contacts"
        :key="index"
        class="flex justify-between items-center p-4 bg-gradient-to-r from-purple-800 via-blue-700 to-gray-900 text-white border border-gray-700 rounded-xl shadow-lg"
      >
        <div>
          <span class="font-bold tracking-wide">{{ contact.name }}</span> - 
          <span class="text-gray-300">{{ contact.phone }}</span>
        </div>
        <div class="flex space-x-3">
          <button
            @click="editContact(index)"
            class="px-4 py-2 bg-gray-700 text-white font-semibold rounded-md hover:bg-gray-600 transition-all"
          >
            Modifica
          </button>
          <button
            @click="confirmRemove(index)"
            class="px-4 py-2 bg-indigo-600 text-white font-semibold rounded-md hover:bg-indigo-500 transition-all"
          >
            Rimuovi
          </button>
        </div>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "ContactList",
  props: {
    contacts: Array,
  },
  data() {
    return {
      isEditing: false,
      editIndex: null,
      editContactData: { name: "", phone: "" },
    };
  },
  methods: {
    confirmRemove(index) {
      const contactName = this.contacts[index].name;
      const contactNumber = this.contacts[index].phone; 
      const confirmed = window.confirm(`Sei sicuro di voler eliminare "${contactName}- ${contactNumber}"?`);
      if (confirmed) {
        this.removeContact(index);
      }
    },
    removeContact(index) {
      this.$emit("removeContact", index);
    },
    editContact(index) {
      this.isEditing = true;
      this.editIndex = index;
      this.editContactData = { ...this.contacts[index] };
    },
    updateContact() {
      this.$emit("updateContact", {
        index: this.editIndex,
        updatedContact: this.editContactData,
      });
      this.cancelEdit();
    },
    cancelEdit() {
      this.isEditing = false;
      this.editIndex = null;
      this.editContactData = { name: "", phone: "" };
    },
  },
};
</script>
