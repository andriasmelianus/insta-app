<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="4">
        <v-card class="elevation-12">
          <v-toolbar color="primary" dark flat>
            <v-toolbar-title
              >Register - {{ this.APPLICATION_NAME }}</v-toolbar-title
            >
            <v-spacer></v-spacer>
          </v-toolbar>

          <v-form @submit.prevent="submitRegistration">
            <v-card-text>
              <v-text-field
                v-model="name"
                :error-messages="invalidInputMessage.name[0]"
                label="Nama"
                name="name"
                prepend-icon="mdi-account"
                type="text"
              ></v-text-field>

              <v-text-field
                v-model="email"
                :error-messages="invalidInputMessage.email[0]"
                label="Email"
                name="email"
                prepend-icon="mdi-email"
                type="text"
              ></v-text-field>

              <v-text-field
                v-model="password"
                :error-messages="invalidInputMessage.password[0]"
                label="Password"
                name="password"
                prepend-icon="mdi-lock"
                type="password"
              ></v-text-field>
              <v-text-field
                v-model="password_confirmation"
                :error-messages="invalidInputMessage.password_confirmation[0]"
                label="Konfirmasi Password"
                name="password_confirmation"
                prepend-icon="mdi-lock"
                type="password"
              ></v-text-field>
            </v-card-text>

            <v-card-actions>
              <v-btn color="primary" type="submit">Daftar</v-btn>
              <v-spacer></v-spacer>
              <v-btn color="default" nuxt to="login"> Kembali </v-btn>
            </v-card-actions>
          </v-form>
        </v-card>
      </v-col>
    </v-row>

    <v-snackbar v-model="registerFail" color="error" :top="true">
      Login gagal
      <br />
      {{ errorMessage }}
    </v-snackbar>
  </v-container>
</template>

<script>
import { MessageHandler } from "~/components/_mixins/message-handler";
export default {
  layout: "default",
  auth: "guest",
  head() {
    return {
      title: "Register",
    };
  },
  mixins: [MessageHandler],

  data: () => ({
    APPLICATION_NAME: process.env.APPLICATION_NAME,
    name: "",
    email: "",
    password: "",
    password_confirmation: "",

    defaultInvalidInputMessage: {
      name: [],
      email: [],
      password: [],
      password_confirmation: [],
    },
    invalidInputMessage: {
      name: [],
      email: [],
      password: [],
      password_confirmation: [],
    },

    registerFail: false,
  }),

  methods: {
    submitRegistration: function () {
      let vm = this;
      vm.clearMessages();
      vm.$axios
        .$post("./api/auth/register", {
          name: vm.name,
          email: vm.email,
          password: vm.password,
          password_confirmation: vm.password_confirmation,
        })
        .then(function (result) {
          vm.$store.commit("notification/show", {
            message:
              "Pendaftaran berhasil! Silahkan login menggunakan data anda.",
            color: "success",
          });
          vm.$router.push("login");
        })
        .catch(function (result) {
          vm.registerFail = true;
          vm.extractMessages(result);
        });
    },
  },
};
</script>
