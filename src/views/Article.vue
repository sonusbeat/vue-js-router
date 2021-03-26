<template>
  <article>
    <Title :text="post.title" />
    <main>{{ post.body }}</main>
  </article>
</template>

<script>
import Title from "@/components/Title";

export default {
  name: "Article",
  components: {
    Title
  },
  data() {
    return {
      post: {}
    };
  },
  methods: {
    async getApi() {
      try {
        const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`);
        const postObject = await data.json();
        this.post = postObject;
      } catch(error) {
        console.error(error);
      }
    }
  },
  created() {
    this.getApi();
  }
}
</script>

<style scoped lang="scss">
h1, main {
  text-align: left;
}
</style>