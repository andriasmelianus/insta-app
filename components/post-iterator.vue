<template>
  <v-data-iterator :items="posts" disable-items-per-page>
    <template v-slot:default="{ items }">
      <v-row>
        <v-col
          v-for="item in items"
          :key="item.name"
          cols="12"
          sm="12"
          md="12"
          lg="12"
        >
          <post-card
            :post_id="item.id"
            :poster="item.user.name"
            :image_url="item.image_url"
            :content="item.content"
            :readableTime="item.name"
            :likesCount="item.likes.length"
            :commentsCount="item.posts.length"
            :likedByMe="false"
            @likeUpdated="updateLike"
          ></post-card>
        </v-col>
      </v-row>
    </template>

    <template v-slot:no-data>
      <v-row>
        <v-col cols="12" sm="12" md="12" lg="12">
          <v-card flat>
            <v-card-title class="headline"
              >Belum ada postingan. Jadilah yang pertama!</v-card-title
            >
          </v-card>
        </v-col>
      </v-row>
    </template>
  </v-data-iterator>
</template>

<script>
import PostCard from "~/components/post/card";
export default {
  props: {
    posts: Array,
  },

  components: {
    PostCard,
  },

  methods: {
    updateLike() {},
  },
};
</script>

<style>
</style>