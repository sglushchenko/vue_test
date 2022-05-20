<template>
  <div class="app">
    <h1>Posts</h1>
    <div class="app_btns">
      <my-button @click="showCreatePostDialog">Create Post</my-button>
      <my-select
        v-model:modelValue="selectedSort"
        :options="sortOptions"
      ></my-select>
    </div>

    <my-dialog v-model:show="isShowCreatePostDialog">
      <edit-post @createPost="createPost" />
    </my-dialog>

    <posts-list :posts="posts" @removePost="removePost" v-if="!isPostLoading" />
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import EditPost from "@/components/EditPost";
import PostsList from "@/components/PostsList";
import axios from "axios";

export default {
  components: {
    EditPost,
    PostsList,
  },
  data() {
    return {
      isShowCreatePostDialog: false,
      isPostLoading: false,
      selectedSort: 'body',
      posts: [],
      sortOptions: [
        { value: "title", name: "Title" },
        { value: "body", name: "Description" },
      ],
    };
  },
  emits: ["removePost1"],
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.isShowCreatePostDialog = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showCreatePostDialog() {
      this.isShowCreatePostDialog = true;
    },
    async fetchPosts() {
      try {
        this.isPostLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );
        this.posts = response.data;
      } catch (e) {
        alert(e);
      } finally {
        this.isPostLoading = false;
      }
    },
    logs() {
      console.log("sdf");
    }
  },
  mounted() {
    this.fetchPosts();
  },
  watch: {
    selectedSort(newValue) {
      console.log(newValue);
    },
    isShowCreatePostDialog(newValue) {
      console.log(newValue);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app_btns {
  margin: 15px;
  display: flex;
  justify-content: space-between;
}
</style>
