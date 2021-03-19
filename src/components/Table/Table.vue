<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="nama"
      sort-by="umur"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="green" dark class="mb-2" v-bind="attrs" v-on="on">
                New User
              </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field
                        v-model="editedItem.nama"
                        required
                        label="Nama"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        v-model="editedItem.umur"
                        label="Umur"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        v-model="editedItem.alamat"
                        label="Alamat"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="dark" text @click="close"> Cancel </v-btn>
                <v-btn color="green" text @click="save"> Save </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-btn small @click="editItem(item)" color="green" class="white--text"
          >Edit</v-btn
        >
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize"> Reset </v-btn>
      </template>
    </v-data-table>

    <v-snackbar v-model="snackbar" timeout="1500">
      Please fill out the form
      <template v-slot:action="{ attrs }">
        <v-btn color="green" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: ["listUser"],
  data: () => ({
    snackbar: false,
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "Nama",
        align: "start",
        sortable: false,
        value: "nama",
      },
      { text: "Umur", value: "umur" },
      { text: "Alamat", value: "alamat" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    nama: [],
    editedIndex: -1,
    editedItem: {
      nama: "",
      umur: 1,
      alamat: "",
    },
    defaultItem: {
      nama: "",
      umur: 1,
      alamat: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New User" : "Edit User";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.nama = this.listUser;
    },

    editItem(item) {
      this.editedIndex = this.nama.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.nama.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.nama.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      console.log(this.editedItem.nama);
      if (this.editedItem.nama == "" || this.editedItem.alamat == "") {
        this.snackbar = true;
      } else {
        if (this.editedIndex > -1) {
          Object.assign(this.nama[this.editedIndex], this.editedItem);
          this.close();
        } else {
          this.nama.push(this.editedItem);
          this.close();
        }
      }
    },
  },
};
</script>