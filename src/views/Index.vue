<template>
  <div>
    <Header />
    <div class="d-flex justify-center">
      <br />
      <Login />
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header/Header.vue";
import Login from "@/components/Form/Login.vue";

export default {
  name: "Index",
  components: {
    Header,
    Login,
  },
};
</script>
