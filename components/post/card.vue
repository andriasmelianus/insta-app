<template>
  <v-card>
    <v-card-title>
      <span class="heading-5">{{ poster }}</span>
    </v-card-title>

    <v-img
      :src="full_image_url + image_url"
      height="300px"
      dark
      v-show="image_url"
    >
    </v-img>

    <v-card-text>{{ content }}</v-card-text>

    <v-card-actions>
      <v-btn plain
        ><span class="caption">{{ readableTime }}</span></v-btn
      >
      <v-spacer></v-spacer>
      <v-btn
        :outlined="!likedByMe"
        rounded
        color="pink lighten-3"
        @click="likeThis(post_id)"
      >
        <v-icon>mdi-heart</v-icon>
        &nbsp; {{ likesCount }}
      </v-btn>
      <v-btn rounded outlined color="cyan">
        <v-icon>mdi-chat</v-icon>
        &nbsp; {{ commentsCount }} comment(s)
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    post_id: Number,
    poster: String,
    image_url: String,
    content: String,
    readableTime: String,

    likesCount: { type: Number, default: 0 },
    commentsCount: { type: Number, default: 0 },

    likedByMe: { type: Boolean, default: false },
  },

  computed: {
    full_image_url: function () {
      return process.env.APPLICATION_API_URL + "/api/image/get/";
    },
  },

  methods: {
    likeThis(postId) {
      let vm = this;
      vm.$axios
        .$post("./api/post/switch-like", {
          post_id: postId,
        })
        .then(function (result) {
          let likeValue = vm.likedByMe;
          likeValue = result.success;
          this.$emit("likeUpdated", likeValue);
        })
        .catch(function (result) {});
    },
  },
};
</script>

<style>
</style>