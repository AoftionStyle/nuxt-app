<template>
  <div class="blog-detail-full" v-if="blog.title">
    <h1>{{ blog.title.rendered }}</h1>
    <p v-html="blog.content.rendered" class="wrap"></p>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: "blog-detail",
  head() {
    // title: function() {
    //   return {
    //     inner: this.title
    //   };
    // },
    return {
      title: this.title
    }
  },
  async asyncData(context) {
    const res = await context.$axios.get(
      "https://blog.skooldio.com/wp-json/wp/v2/posts/" + context.route.params.id
    );
    console.log('res: ', res);
    return {
      blog: res.data,
      title: res.data.title.rendered
    }
  },
  async mounted() {
  },
  methods: {
    ...mapActions(["changeHeader"])
  }
};
</script>

<style>
.blog-detail {
  width: 80%;
  margin-left: auto;
  margin-right: auto;
}
.wrap {
  width: 100%;
}
img {
  max-width: 100%;
}
</style>
