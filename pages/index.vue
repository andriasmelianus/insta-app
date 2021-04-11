<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12" sm="12" md="12" lg="12">
        <v-card>
          <v-card-text>
            <v-file-input
              :rules="rules"
              accept="image/*"
              placeholder="Ambil sebuah foto"
              prepend-icon="mdi-camera"
              label="Foto"
              v-model="image_file"
            ></v-file-input>
            <v-textarea
              auto-grow
              rows="2"
              outlined
              v-model="post_content"
            ></v-textarea>
            <v-btn color="primary" outlined rounded @click="post">
              <v-icon>mdi-send</v-icon>
              POST
            </v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <post-iterator v-bind:posts="items"></post-iterator>
  </v-container>
</template>

<script>
import PostCard from "~/components/post/card";
import PostIterator from "~/components/post-iterator";
export default {
  layout: "dashboard",

  components: {
    PostCard,
    PostIterator,
  },

  mounted() {
    this.reloadPosts();
  },

  data: () => ({
    rules: [
      (value) =>
        !value ||
        value.size < 2000000 ||
        "Image size should be less than 2 MB!",
    ],

    post_content: "",
    image_file: [],

    items: [],
  }),

  methods: {
    reloadPosts() {
      let vm = this;
      vm.$axios
        .$get("./api/post/all")
        .then(function (result) {
          vm.items = result;
        })
        .catch(function (result) {});
    },
    post() {
      let vm = this;
      const formData = new FormData();
      formData.append("image_file", this.image_file);
      formData.append("content", this.post_content);

      vm.$axios
        .$post("./api/post/store", formData)
        .then(function (result) {})
        .catch(function (result) {});
    },
  },
};
</script>
