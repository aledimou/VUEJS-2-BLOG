<template>
  <div class="" id="single-blog">
    <h1>{{ blog.title }}</h1>
    <article>{{ blog.content }}</article>
    <br />
    <i
      ><p>Written by {{ blog.author }}</p></i
    >
  </div>
</template>

<script>
export default {
  name: "singleBlog",
  data() {
    return {
      id: this.$route.params.id,
      blog: {},
    };
  },
  created() {
    this.$http
      .get(
        "https://vue-blog-f16a4-default-rtdb.firebaseio.com/posts/" +
          this.id +
          ".json"
      )
      .then((res) => {
        console.log(res);
        return res.json();
      })
      .then((data) => {
        this.blog = data;
      });
  },
};
</script>

<style>
#single-blog {
  max-width: 960px;
  margin: 0 auto;
}
</style>