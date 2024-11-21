<template>
  <form @submit.prevent="addContact" class="space-y-6 bg-gradient-to-r from-gray-800 via-gray-700 to-gray-600 p-6 rounded-xl shadow-lg">
    <input
      type="text"
      v-model="newContact.name"
      placeholder="Nome"
      class="w-full p-3 border border-gray-500 rounded-lg bg-gray-800 text-gray-300 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-400"
    />
    <br>
    <input
      type="tel"
      v-model="newContact.phone"
      placeholder="Numero"
      class="w-full p-3 border border-gray-500 rounded-lg bg-gray-800 text-gray-300 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-400"

    />
    <br>
    <button type="submit"
    class="w-full py-3 bg-blue-500 text-white font-semibold rounded-lg hover:bg-blue-400 transition-all"
    >Aggiungi Contatto</button>
    <p v-if="errorMessage" class="text-red-500 text-sm text-center">{{ errorMessage }}</p>
  </form>
</template>

<script>
export default {
  name: "AddContactForm",
  data() {
    return {
      newContact: {
        name: "",
        phone: "",
      },
      errorMessage: "",
    };
  },
  methods: {
    addContact() {
      if (!this.newContact.name && !this.newContact.phone) {
        this.errorMessage = "I campi sono vuoti!";
        return;
      }
      if (!this.newContact.name || !this.newContact.phone) {
        this.errorMessage = "Entrambi i campi sono obbligatori!";
        return;
      }
      this.errorMessage = "";
      this.$emit("addContact", { ...this.newContact });
      this.newContact.name = "";
      this.newContact.phone = "";
    }
  }
}
</script>