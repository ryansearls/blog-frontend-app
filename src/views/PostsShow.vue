<template>
  <div class="posts-show">
    <div class="container">
      <h2>{{ post.title }}</h2>
      <h2>{{ post.body }}</h2>
      <img v-bind:src="post.image" alt="post.title" />
      <router-link v-bind:to="`/posts/${rpost.id}/edit`"><button>Edit postsindex</button></router-link>
      <router-link to="/posts">Back to Posts</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
};
</script>
