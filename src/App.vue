<template>
  <div>
    <app-header></app-header>
    <router-view></router-view>
  </div>
</template>

<script>
// Imports
import addBlog from "./components/addBlog.vue";
import showBlogs from "./components/showBlogs.vue";
import appheader from "./components/appHeader.vue";
import singleBlog from "./components/singleBlog.vue";

export default {
  components: {
    "add-blog": addBlog,
    "show-blocks": showBlogs,
    "app-header": appheader,
    "single-blog": singleBlog,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style>
body {
  margin: 0;
  font-family: "Nunito SemiBold";
}
</style>
