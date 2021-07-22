<template>
  <div class="posts-edit">
    <form v-on:submit:prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="currentPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="currentPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
      <button v-on:click="destroyPost()">Delete</button>
    </form>
    <div class="container">
      <h2>{{ post.title }}</h2>
      <h2>{{ post.body }}</h2>
      <img v-bind:src="post.image" alt="post.title" />
      <router-link to="/posts">Back to Posts</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      console.log("posts show", response);
      this.post = response.data;
    });
  },
  methods: {
    updatePost: function (post) {
      var editPostParams = post;
      axios
        .patch("/posts/" + post.id, editPostParams)
        .then((response) => {
          console.log("post update", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("posts update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
