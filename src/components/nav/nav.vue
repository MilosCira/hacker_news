<template>
  <v-container>
    <v-app-bar absolute flat color="indigo"  dark>
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

    <router-link to="/">  <v-toolbar-title class="white--text">FPMOZ</v-toolbar-title></router-link>
    </v-app-bar>

    <v-navigation-drawer color="indigo" v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon color="white">mdi-home</v-icon>
            </v-list-item-icon>
          <router-link to="/">  <v-list-item-title class="white--text">Home</v-list-item-title></router-link>
          </v-list-item>
              
              <v-list-item>
            <v-list-item-icon>
              <v-icon color="white">mdi-newspaper</v-icon>
            </v-list-item-icon>
            <router-link to="/News">  <v-list-item-title class="white--text">Vesti</v-list-item-title></router-link>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon>
              <v-icon color="white">mdi-magnify</v-icon>
            </v-list-item-icon>
            <router-link to="/search-by-date">  <v-list-item-title class="white--text">Filtriraj vesti po datumu</v-list-item-title></router-link>
          </v-list-item>

          
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      group: null,
    };
  },
};
</script>

<style scoped>
a{
    text-decoration: none;
    color: white;
}
</style>