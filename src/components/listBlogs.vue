<template>
  <div id="show-blogs">
    <h1>List Blog Titles</h1>
    <input type="text" v-model="search" placeholder="Search Blogs..." />
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h2>{{ blog.title }}</h2>
    </div>
  </div>
</template>

<script>
//Imports
    import searchMixin from '../mixins/searchMixin';
//Exports
export default {
  components: {},
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  methods: {},
  //Life-Cycle Hooks
  created() {
    //request to GET data from my database
    this.$http
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(function(data) {
        //console.log(data);
        //store the fetched data in my blogs property (under data())
        this.blogs = data.body.slice(0, 10);
      });
  },
  computed: {

    },
    filters: {
      toUppercase(value) {
        return value.toUpperCase();
      }
    },
    directives: {
      rainbow: {
        bind(el, binding, vnode) {
          //Making the style random using the math object (returning a 6digit random number)
          el.style.color =
            "#" +
            Math.random()
              .toString()
              .slice(2, 8);
        }
      }
    },
    mixins: [searchMixin]
};
</script>

<style scoped>
body {
    font-family: 'Roboto', sans-serif;
}
#show-blogs {
  max-width: 800px;
  margin: 0px auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
