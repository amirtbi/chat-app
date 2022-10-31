<script setup>
// Constants
const drawer = ref(true);

const navItems = ref([
  { text: "Home", link: "/", icon: "mdi-view-dashboard" },
  { text: "Chat", link: "/chat", icon: "mdi-forum" },
]);

// Functions

const showMessage = (route) => {
  navigateTo(route);
};
</script>

<template>
  <!-- App.vue -->

  <v-app>
    <v-navigation-drawer color="#151529" app v-model="drawer" flat>
      <v-divider></v-divider>

      <v-list class="pa-4" color="white" density="compact" nav>
        <v-list-item
          :prepend-icon="nav.icon"
          v-for="(nav, index) in navItems"
          :key="index"
          :value="nav.text"
          :title="nav.text"
          @click="showMessage(nav.link)"
        >
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <template v-slot:prepend>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </template>

      <v-app-bar-title>Chat App</v-app-bar-title>
    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main min-height="100%">
      <!-- Provides the application the proper gutter -->
      <v-container height="100%" fluid>
        <slot />
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<style scoped>
.v-list-item {
  color: #ffff;
}
</style>
