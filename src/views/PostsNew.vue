<template>
  <div class="posts-new">
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
        <input type="text" v-model="newPostParams.chef" />
      </div>
      <div>
        <label>Directions:</label>
        <input type="text" v-model="newPostParams.directions" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image_url" />
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
    };
  },
  methods: {
    createPost: function () {
      axios.post("/posts/new", this.newPostParams).then((response) => {
        this.$router.push("/recipes");
        console.log(response.data);
      });
    },
  },
};
</script>
