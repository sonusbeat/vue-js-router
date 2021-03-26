<template>
  <Title text="Blog" />


  <article v-if="arrayBlog.length > 0">
    <p v-for="item in arrayBlog" :key="item.id">
      <router-link :to="`/blog/${item.id}`">
        {{ item.title }}
      </router-link>
    </p>
  </article>

  <p v-else>¡ Aún no hay datos !</p>
</template>

<script>
import Title from "@/components/Title";

export default {
  name: 'Blog',
  components: {
    Title
  },
  data() {
    return {
      arrayBlog: []
    }
  },
  methods: {
    async getApi() {
      try {
        const data = await fetch("https://jsonplaceholder.typicode.com/posts");
        const array = await data.json();
        this.arrayBlog = array;
      } catch (error) {
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
  ol {
    text-align: left;
  }
  a {
    font-weight: bold;
    color: #42b983;
    text-decoration: none;

    &:hover {
      color: orange;
    }
  }
</style>
