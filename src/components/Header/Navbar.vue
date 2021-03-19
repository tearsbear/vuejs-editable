<template>
  <v-app-bar color="green" max-width="900" dark elevation="0">
    <v-toolbar-title>Dashboard</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn text to="/"> Logout </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "Navbar",
};
</script>