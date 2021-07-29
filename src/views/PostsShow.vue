<template>
  <div class="posts-show">
    <div class="container">
      <h2>{{ post.title }}</h2>
      <h2>{{ post.body }}</h2>
      <!-- <img v-bind:src="post.image" alt="post.title" /> -->
      <li v-if="$parent.getUserId() == post.user_id">
        <router-link v-bind:to="`//${post.id}/edit`"><button>Edit Post</button></router-link>
      </li>
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
      console.log(response.data);
    });
  },
};
</script>
