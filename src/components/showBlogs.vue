<template>
  <div v-theme:column="narrow" class="showBlogs" id="show-blogs">
    <h1>All blog Articles</h1>
    <input type="text" v-model="search" placeholder="search a blog" />
    <div class="single-blog" v-for="post in filteredPosts" :key="post.id">
      <router-link :to="'/blog/' + post.id"
        ><h2>{{ post.title | uppercase }}</h2>
      </router-link>
      <article>{{ post.content }}</article>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: [],
      wide: "wide",
      narrow: "narrow",
      search: "",
    };
  },
  computed: {
    filteredPosts: function () {
      return this.blogs.filter((post) => {
        return post.title.match(this.search);
      });
    },
  },
  created() {
    this.$http
      .get("https://vue-blog-f16a4-default-rtdb.firebaseio.com/posts.json")
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        let blogArray = [];
        for (let key in data) {
          data[key].id = key;
          blogArray.push(data[key]);
        }
        this.blogs = blogArray;
      });
  },
  //locally filter
  filters: {
    uppercase(value) {
      return value.slice(0, 100) + "...";
    },
  },
};
</script>

<style>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px;
  box-sizing: border-box;
  background: #eee;
}
</style>