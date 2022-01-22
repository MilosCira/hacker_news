<template>
  <div class="news-search mt-9">
    <v-card class="pa-md-4 mx-lg-auto" color="white" width="500px">
      <v-menu
        v-if="searchByDate"
        v-model="menu"
        :close-on-content-click="false"
        :nudge-right="40"
        transition="scale-transition"
        offset-y
        min-width="290px"
      >
        <template v-slot:activator="{ on }">
          <v-text-field
            :value="currentDate"
            label="Pretrazi po datumu"
            readonly
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          :disabled="isError || isLoading"
          :value="currentDate"
          @input="value => onChange(value, 'date')"
        ></v-date-picker>
      </v-menu>
      <v-text-field
        solo
        :clearable="!isError && !isLoading"
        :readonly="isError || isLoading"
        :value="query"
        placeholder="Pretrazi vesti"
        @input="value => onChange(value, 'query')"
      ></v-text-field>
    </v-card>
  </div>
</template>

<script>
import { mapState } from "vuex";
import debounce from "lodash.debounce";
export default {
  name: "NewsSearch",
  data: () => ({
    menu: false,
    query: "",
    currentDate: ""
  }),
  computed: {
    searchByDate() {
      return this.$route.path === "/search-by-date";
    },
    ...mapState(["isError", "isLoading"])
  },
  methods: {
    onChange: debounce(function(value, type) {
      this.currentDate = type === "date" ? value : this.currentDate;
      this.query = type === "query" ? value : this.query;
      this.menu = false;
      this.$store.dispatch("FETCH_NEWS_LIST", {
        query: this.query,
        page: 1,
        date: this.currentDate
      });
    }, 250)
  }
};
</script>

<style scoped>
input {
  margin: 5px 0;
}
</style>