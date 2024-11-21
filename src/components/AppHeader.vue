<template>
  <header
    class="rounded-b-3xl bg-gradient-to-r from-purple-800 via-blue-700 to-gray-900 p-6 shadow-lg">
    <div class="flex items-center justify-between">
      <h1 class="text-2xl font-bold text-gray-100 tracking-wide">📞 Gestione Contatti</h1>
      <div class="flex items-center space-x-3">  
        <input
          type="text"
          v-model="searchQuery"
          @input="onSearch"
          placeholder="Cerca ..."
          class="w-64 p-2 rounded-md border border-gray-600 bg-gray-800 text-gray-300 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-blue-400"
        />
        <span class="text-2xl">🔍</span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    onSearch() {
      this.$emit("updateSearch", this.searchQuery);
    },
  },
};
</script>
