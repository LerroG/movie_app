<template>
  <div id="app">
    <LoaderComp />
    <NotificationToast />
    <PosterBg :poster="posterBg" />
    <MainHeader />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <MoviesPagination
      :current-page="currentPage"
      :per-page="moviesPerPage"
      :total="moviesLength"
      @pageChanged="onPageChanged"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "@/components/MoviesList.vue";
import PosterBg from "@/components/PosterBg.vue";
import MoviesPagination from "@/components/MoviesPagination.vue";
import LoaderComp from "@/components/LoaderComp.vue";
import MainHeader from "@/components/MainHeader.vue";
import NotificationToast from "@/components/NotificationToast.vue";

export default {
  name: "App",
  components: {
    MoviesList,
    PosterBg,
    MoviesPagination,
    LoaderComp,
    MainHeader,
    NotificationToast,
  },
  data: () => ({
    posterBg: "",
  }),
  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "currentPage",
      "moviesPerPage",
      "moviesLength",
    ]),
  },
  watch: {
    "$route.query": {
      handler: "onPageQueryChange",
      immediate: true,
      deep: true,
    },
  },
  methods: {
    ...mapActions("movies", ["changeCurrentPage"]),

    onPageQueryChange({ page = 1 } = {}) {
      this.changeCurrentPage(Number(page));
    },
    onChangePoster(poster) {
      this.posterBg = poster;
    },
    onPageChanged(page) {
      this.$router.push({ query: { page } });
      // this.changeCurrentPage(page);
    },
  },
  // created() {
  //   if (this.$route.query.page) {
  //     this.changeCurrentPage(Number(this.$route.query.page));
  //   }
  // },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  min-height: 100vh;
}
</style>
