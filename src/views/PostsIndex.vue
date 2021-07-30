<template>
  <div class="posts-index">
    <div class="card-deck">
      <div class="card">
        <div
          v-for="post in posts"
          :key="post.id"
          v-bind:class="{ selected: post === currentPost }"
          v-on:click="currentPost = post"
        >
          <img class="card-img-top" v-bind:src="post.image" alt="Card image cap" />
          <div class="card-body">
            <h5 class="card-title">Title: {{ post.title }}</h5>
            <p class="card-text">Body: {{ post.body }}</p>
            <p class="card-text"><small class="text-muted"></small></p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- <div v-for="post in posts" :key="post.id">
      <router-link v-bind:to="`/posts/${post.id}`">
        <h2>Title: {{ post.title }}</h2>
        <p>Chef: {{ post.body }}</p>
        <img v-bind:src="post.image" alt="post.title" />
      </router-link>
    </div>
  </div> -->
</template>

<style>
.card {
  width: 50%;
}
.selected {
  color: white;
  background-color: purple;
  transition: background-color 1s ease;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  data: function () {
    return {
      message: "Here are posts!",
      posts: [],
      currentPost: {},
    };
  },
  mixins: [Vue2Filters.mixin],
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts:", this.posts);
      });
    },
  },
};
</script>
