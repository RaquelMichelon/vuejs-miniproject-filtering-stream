<template>
  <div class="container">
    <div class="half">
      <Filters
        :filterPosts="filterPosts"
        :search="search"
        :filteredPosts="filteredPosts"
      />
    </div>
    <div class="half">
      <Posts :posts="posts" />
    </div>
  </div>
</template>

<script>
import Filters from "./components/Filters.vue";
import Posts from "./components/Posts.vue";

import MOCK_DATA from "./MOCK_DATA.json";

export default {
  name: "App",
  components: {
    Filters,
    Posts,
  },
  data() {
    return {
      posts: MOCK_DATA,
    };
  },
  methods: {
    filterPosts(categoryName) {
      this.resetPosts();
      if (categoryName !== "All") {
        this.posts = this.posts.filter((post) => {
          return post.category === categoryName;
        });
      }
    },
    search(term) {
      this.resetPosts();
      this.posts = this.posts.filter((post) => {
        return post.title.toLowerCase().includes(term.toLowerCase());
      });
    },
    resetPosts() {
      this.posts = MOCK_DATA;
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;

  margin: 3rem;
}
.half {
  width: 50%;
}
</style>
