<template>
  <div v-if="posts.length > 0">
    <h3>Posts</h3>
    <post-item
      v-for="post in posts"
      :key="post.id"
      :post="post"
      @removePost="$emit('removePost', post)"
    />
  </div>
  <h2 v-else style="color: red;">You don't have posts</h2>
</template>

<script>
import PostItem from "./PostItem.vue";
export default {
  components: { PostItem },
  emits: ["removePost"],
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
</style>