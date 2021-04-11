<template>
  <v-app id="inspire">
    <v-app-bar app dense color="white">
      <v-toolbar-title>Insta App</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn color="blue" outlined rounded class="mx-1" nuxt to="/">
        <v-icon>mdi-newspaper</v-icon>
        Beranda
      </v-btn>

      <v-btn color="blue" outlined rounded class="mx-1" nuxt to="liked">
        <v-icon>mdi-heart</v-icon>
        Disukai
      </v-btn>

      <v-btn color="blue" outlined rounded class="mx-1" nuxt to="commented">
        <v-icon>mdi-chat</v-icon>
        Dikomentari
      </v-btn>

      <v-spacer></v-spacer>
      <user-menu></user-menu>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col cols="12" sm="3">
            <v-sheet rounded="lg" min-height="268">
              <dashboard-leftbar-card></dashboard-leftbar-card>
            </v-sheet>
          </v-col>

          <v-col cols="12" sm="6">
            <v-sheet min-height="90vh" rounded="lg">
              <nuxt />
            </v-sheet>
          </v-col>

          <v-col cols="12" sm="3">
            <v-sheet rounded="lg" min-height="268">
              <dashboard-rightbar-card></dashboard-rightbar-card>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>

      <footer-section></footer-section>
    </v-main>
  </v-app>
</template>

<script>
import UserMenu from "~/components/_dashboard/user-menu";
import DashboardLeftbarCard from "~/components/dashboard-leftbar-card";
import DashboardRightbarCard from "~/components/dashboard-rightbar-card";
import FooterSection from "~/components/_dashboard/footer";
export default {
  layout: "default",

  components: {
    UserMenu,

    DashboardLeftbarCard,
    DashboardRightbarCard,

    FooterSection,
  },

  data: () => ({}),
};
</script>
