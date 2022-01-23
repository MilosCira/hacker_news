<template>
<v-app>
  <NavBar></NavBar>
  <v-main>
      <router-view />
  </v-main>
  <Footer></Footer>
</v-app>
</template>
<script>
import NavBar from "@/components/nav/nav"
import Footer from "@/components/footer/footer"
export default {
  components:{
    Footer,
    NavBar
  },
  data() {
    return {
      news:[]
    };
  },
  methods:{
     getNews() {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.news = this.$store.getters.fetchJobs;
      console.log(this.news);
      return this.news;
    },
  },
  mounted(){
   
    this.getNews();
  }
  
  
};
</script>