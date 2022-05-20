<template>
  <form @submit.prevent>
    <h4>Create post</h4>
    <my-input
      v-model="post.title"
      @input="post.title = $event.target.value"
      type="text"
      placeholder="Title"
    />
    <my-input
      v-model="post.description"
      @input="post.description = $event.target.value"
      type="text"
      placeholder="Description"
    />
    <my-button class="btn" style="align-self: flex-end; margin-top: 25px;" @click="createPost">Create</my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        id: Date.now(),
        title: "",
        description: "",
      },
    };
  },
  methods: {
    createPost() {
      if (this.post.title.length == 0) {
        return;
      }
      if (this.post.description.length == 0) {
        return;
      }

      this.post.id = Date.now();
      this.$emit("createPost", this.post);

      this.post = {
        id: Date.now(),
        title: "",
        description: "",
      };
    },
  },
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
}
</style>