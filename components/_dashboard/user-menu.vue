<template>
  <v-menu offset-y>
    <template v-slot:activator="{ on, attrs }">
      <v-btn icon color="blue darken-2" v-bind="attrs" v-on="on">
        <v-icon>mdi-account</v-icon>
      </v-btn>
    </template>

    <v-list>
      <v-list-item nuxt to="privacy">Privasi</v-list-item>
      <v-list-item nuxt to="setting">Pengaturan</v-list-item>
      <v-list-item nuxt to="logout">Logout</v-list-item>
    </v-list>
  </v-menu>
</template>

<script>
export default {
  computed: {
    user_name: function () {
      return this.$auth.user.name;
    },
  },
};
</script>
