<template>
  <div>
    <div class="d-flex justify-center green">
      <Navbar />
    </div>
    <Header />
    <div class="container" style="margin-top: -100px">
      <Table :listUser="listUser" />
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Header/Navbar.vue";
import Header from "@/components/Header/Header.vue";
import Table from "@/components/Table/Table.vue";

export default {
  name: "Home",
  components: {
    Navbar,
    Header,
    Table,
  },
  data: () => ({
    listUser: [
      {
        nama: "Jeihan",
        umur: 20,
        alamat: "Jakarwwhj",
      },
    ],
  }),
};
</script>
