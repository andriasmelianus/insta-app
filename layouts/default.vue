<template>
  <v-app>
    <v-main>
      <nuxt />

      <notification></notification>
    </v-main>
  </v-app>
</template>

<script>
import Notification from "~/components/_support/notification";
export default {
  components: {
    Notification,
  },
};
</script>

<style>
</style>