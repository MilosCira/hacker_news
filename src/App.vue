<template>
<v-app>
  <NavBar></NavBar>
  <v-content>
      <router-view />
  </v-content>
  <Footer></Footer>
</v-app>
</template>
<script>
import axios from 'axios'
import NavBar from "@/components/nav/nav"
import Footer from "@/components/footer/footer"
export default {
  components:{
    Footer,
    NavBar
  },
  data() {
    return {
      perPage: 30,
      posts: null,
      selectedIdx: -1,
      selectedStory: null,
    };
  },
  computed: {
            selectedPost() {
                return this.selectedIdx === null ? -1 : this.posts[this.selectedIdx]
            }
        },
        methods: {
            viewStory() {
                this.selectedStory = this.posts[this.selectedIdx];
            },
        },
  mounted() {
    axios.get('https://hacker-news.firebaseio.com/v0/topstories.json')
              .then(response => {
                  this.posts = response.data.slice(0, this.perPage - 1)
                  console.log(this.posts);
              })
  },
};
</script>