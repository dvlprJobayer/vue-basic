<template>
  <button @click="addPost" style="margin-top: 1rem; margin-left: 1rem">
    Add Post
  </button>
  <h1>All</h1>
  <ul>
    <SinglePost
      v-for="post in posts"
      :post="post"
      :key="post.id"
      @delete="handleDelete"
      @fav-post="handleFavPost"
    />
  </ul>
  <br />
  <h1>Favs</h1>
  <ul>
    <SinglePost
      v-for="post in favs"
      :post="post"
      :key="post.id"
      @delete="handleDelete"
      @fav-post="handleFavPost"
    />
  </ul>
  <br />
  <h1>UnFavs</h1>
  <ul>
    <SinglePost
      v-for="post in unFavs"
      :post="post"
      :key="post.id"
      @delete="handleDelete"
      @fav-post="handleFavPost"
    />
  </ul>
</template>

<script>
import SinglePost from "../components/SinglePost.vue";
export default {
  components: {
    SinglePost,
  },
  computed: {
    favs() {
      return this.posts.filter((post) => post.fav);
    },
    unFavs() {
      return this.posts.filter((post) => !post.fav);
    },
  },
  methods: {
    handleDelete(id) {
      this.posts = this.posts.filter((post) => post.id !== id);
    },
    handleFavPost(id) {
      const post = this.posts.find((post) => post.id === id);
      post.fav = !post.fav;
    },
    addPost() {
      this.posts.push({
        id: Math.random().toString(),
        title: "Post " + (this.posts.length + 1),
        fav: false,
      });
    },
  },
  data() {
    return {
      posts: [
        {
          id: 1,
          title: "Post 1",
          fav: true,
        },
        {
          id: 2,
          title: "Post 2",
          fav: false,
        },
        {
          id: 3,
          title: "Post 3",
          fav: true,
        },
      ],
    };
  },
};
</script>
<style scoped>
h1 {
  color: green;
}
</style>
