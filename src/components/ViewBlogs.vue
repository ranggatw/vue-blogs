<template>
  <div v-theme="themeSize" class="blog-list">
    <div class="btns">
      <v-btn v-on:click="wide">Wide</v-btn>
      <v-btn v-on:click="narrow">Narrow</v-btn>
      <v-pagination v-model="blog" :length="6"></v-pagination>
    </div>


    <h2 class="titleBlog">Blog Posts</h2>
    <v-card v-for="blog in filteredBlogs" class="single-blog" :key="blog.id">
      <router-link v-bind:to="'/blog/' + blog.id">
        <v-card-title v-ranbow>{{ blog.title }}</v-card-title>
      </router-link>
      <v-card-text>{{ blog.description | snippet }}</v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "ViewBlogs",
  data() {
    return {
      blogs: [],
      search: "",
      themeSize: "narrow",
      page: 1,
      pageSize: 10,
      pages: [],
    };
  },
  methods: {
    wide() {
      this.themeSize = "wide";
    },
    narrow() {
      this.themeSize = "narrow";
    },
  },
  computed: {
    filteredBlogs() {
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search);
      }
      );
    },
  },
  created() {
    this.$http
      .get("https://vuejs-blog-app-9ebdf.firebaseio.com/posts.json")
      .then((response) => {
        var blogsArray = [];
        for (let key in response.data) {
          response.data[key].id = key;
          blogsArray.push(response.data[key]);
        }
        this.blogs = blogsArray;
      });
  },
  filters: {
    snippet(value) {
      return value.slice(0, 200) + " ...";
    },
  },
  directives: {
    ranbow: {
      bind(el) {
        el.style.color = "#" + Math.random().toString().slice(2, 8);
      },
    },
    theme(el, binding) {
      if (binding.value == "wide") {
        el.style.maxWidth = "1200px";
      } else if (binding.value == "narrow") {
        el.style.maxWidth = "600px";
      }
    },
  },
};
</script>

<style scoped>
.blog-list {
  position: relative;
  box-sizing: border-box;
  max-width: 800px;
  margin: 20px auto;
  padding: 20px 0;
}

.titleBlog {
  margin-bottom: 60px;
}

.single-blog {
  background: #f5f6f7;
  margin: 30px auto 10px;
  padding: 15px;
}

.btns {
  display: flex;
  position: absolute;
  right: 0;
  top: 55px;
}
</style>
