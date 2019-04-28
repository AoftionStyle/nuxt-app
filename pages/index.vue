<template>
  <div class="home">
    <ul>
      <li v-for="blog in blogs" :key="blog.id">
        <nuxt-link
          :to="{
            name: 'blog-id',
            params: {
              id: blog.id
            }
          }"
          >{{ blog.title.rendered }}</nuxt-link
        >
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  async asyncData (context) {
    const res = await context.$axios.get("https://blog.skooldio.com/wp-json/wp/v2/posts/")
    return {
      blogs: res.data
    }
  },
  // async mounted() {
  //   const res = await axios.get("https://blog.skooldio.com/wp-json/wp/v2/posts/")
  //   this.blogs = res.data
  // },
};
</script>

<style>
li {
  list-style: none;
}
</style>
