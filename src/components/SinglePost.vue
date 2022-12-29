<template>
  <li>
    <div :class="{ fav: post.fav }" style="display: inline-block">
      {{ post.title }}
    </div>
    |
    <button @click="handleClick">Delete</button> |
    <button @click="$emit('fav-post', post.id)">Fav Post</button>
  </li>
</template>

<script>
export default {
  props: ["post"],
  methods: {
    handleClick() {
      this.$emit("delete", this.post.id);
    },
  },
};
</script>

<style scoped>
.fav {
  color: blue;
}
</style>
