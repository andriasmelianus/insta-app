<template>
  <v-card max-width="375" class="mx-auto">
    <v-img
      src="https://cdn.vuetifyjs.com/images/lists/ali.png"
      height="300px"
      dark
    >
    </v-img>

    <v-list two-line>
      <v-list-item>
        <v-list-item-icon>
          <v-icon color="indigo"> mdi-account </v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>{{ user_name }}</v-list-item-title>
          <v-list-item-subtitle>{{ user_email }}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item>
        <v-list-item-icon>
          <v-icon color="indigo"> mdi-phone </v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>(650) 555-1234</v-list-item-title>
          <v-list-item-subtitle>Mobile</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-list>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn plain nuxt to="/edit/profile">Edit</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  computed: {
    user_name: function () {
      return this.$auth.user.name;
    },
    user_email: function () {
      return this.$auth.user.email;
    },
  },
};
</script>

<style>
.sticky-card {
  width: 344px;
  position: fixed;
  top: 90px;
  z-index: 1;
  /* centering */
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
}
</style>