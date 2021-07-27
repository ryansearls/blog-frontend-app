<template>
  <div class="posts-new">
    <img v-if="status" :src="`https://http.cat/${status}`" />
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <small>
          v-if="newPostParams.body.length > 150" class="text-danger"> There are
          {{ 150 - newPostParams.body.length }} characters remaining.
        </small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      newPostParams: {},
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          this.$router.push("/posts");
          console.log(response.data);
        })
        .catch((error) => {
          this.errors = error.response.status;
        });
    },
  },
};
</script>
