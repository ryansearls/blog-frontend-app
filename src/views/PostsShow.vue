<template>
  <div class="posts-show">
    <div class="container">
      <h2>{{ post.title }}</h2>
      <h2>{{ post.body }}</h2>
      <h2>{{ post.image }}</h2>
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
    axios.get("/posts/1").then((response) => {
      this.post = response.data;
    });
  },
};
</script>
