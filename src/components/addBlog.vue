<template>
  <div id="add-blog">
    <div v-if="!submited">
      <h2>Add a New Blog Post</h2>
      <form>
        <label>Blog Title:</label>
        <input type="text" v-model.lazy="blog.title" required />
        <label>Blog Content:</label>
        <textarea v-model.lazy.trim="blog.content"></textarea>
        <div class="" id="checkboxes">
          <label>Ninjas</label>
          <input type="checkbox" value="ninjas" v-model="blog.categories" />
          <label>Wizards</label>
          <input type="checkbox" value="wizards" v-model="blog.categories" />
          <label>Mario</label>
          <input type="checkbox" value="mario" v-model="blog.categories" />
          <label>Cheese</label>
          <input type="checkbox" value="cheese" v-model="blog.categories" />
        </div>
        <label>Author</label>
        <select id="selectbox" v-model="blog.author">
          <option value="" disabled selected hidden>Choose an author</option>
          <option v-for="name in authorLIst" :key="name">
            {{ name }}
          </option>
        </select>
        <button type="submit" @click.prevent="postData">Submit</button>
      </form>
    </div>
    <div class="" v-if="showSubmitMessage">Submited Succesfully</div>
    <div id="preview">
      <h3>Preview blog</h3>
      <p>Blog title: {{ blog.title }}</p>
      <p>Blog content:</p>
      <p style="white-space: pre">{{ blog.content }}</p>
      <p>Blog Categories</p>
      <ul>
        <li v-for="category in blog.categories" :key="category">
          {{ category }}
        </li>
      </ul>
      <p>Author: {{ blog.author }}</p>
    </div>
  </div>
</template>

<script>
// Imports

export default {
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
      },
      authorLIst: ["alex", "miriam", "nick", "john", "cedric"],
      submited: false,
      showSubmitMessage: false,
    };
  },
  methods: {
    clearSubmitMessage() {
      setTimeout(() => {
        this.showSubmitMessage = false;
      }, 4000);
    },
    postData() {
      this.$http
        .post(
          "https://vue-blog-f16a4-default-rtdb.firebaseio.com/posts.json",
          this.blog
        )
        .then((response) => {
          console.log(response);
          this.submited = true;
          this.showSubmitMessage = true;
          this.clearSubmitMessage();
        });
    },
  },
};
</script>

<style>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}

#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
label {
  display: inline-block;
}
</style>
