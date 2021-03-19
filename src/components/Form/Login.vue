<template>
  <div class="bg-form elevation-1">
    <h1>Welcome back👋</h1>
    <p class="form-desc">login to your account.</p>
    <v-text-field
      color="green"
      label="Username"
      outlined
      class="mt-5"
    ></v-text-field>
    <v-text-field
      color="green"
      label="Password"
      outlined
      class="mt-5"
    ></v-text-field>
    <v-btn to="home" color="green" class="white--text">login</v-btn>
  </div>
</template>

<script>
export default {
  name: "Login",
};
</script>

<style scoped>
.bg-form {
  background-color: white;
  height: auto;
  margin-top: 50px;
  border-radius: 10px;
  text-align: left;
  padding: 30px;
  width: 400px;
  margin-top: -80px;
}

.bg-form p {
  font-size: 18px;
  font-weight: 500;
  margin-top: -5px;
}
</style>