<template>
  <div class="single-blog">
    <h2> Single Blog Post </h2>
    <v-card class="blog-content">
      <v-card-title>{{ blog.title }}</v-card-title>
      <v-card-text>{{ blog.description }}</v-card-text>
      <v-card-text> <strong>Author: </strong> {{ blog.author }}</v-card-text>
      <v-card-text> <strong>Catagory: </strong>
        <ul>
          <li v-for="category in blog.categories" v-bind:key="category">{{ category }}</li>
        </ul>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>


export default {
  name: 'SingleBlog',
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    }
  },
  created() {
    this.$http.get('https://vuejs-blog-app-9ebdf.firebaseio.com/posts/' + this.id + '.json').then((response) => {
      this.blog = response.data;
    });
  },
}
</script>

<style scoped>
.single-blog {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
}

.blog-content {
  background: #f5f6f7;
  margin: 20px auto;
  padding: 20px;
}
</style>
