<template>
  <section class="bg-black-500 text-white justify-center md:mx-0">
    <Navbar />
    <!-- card List  -->
    <div class="w-full px-28 py-8">
      <SearchBody :url-film-anime="urlFilm" :title-film-anime="titleAnime" />
    </div>

    <Footer />
  </section>
</template>

<script lang="ts">
import Vue from 'vue';
import VueRouter from 'vue-router';
import SearchBody from './Reusable/SearchBody.vue';
Vue.use(VueRouter);

export default Vue.extend({
  components: {
    SearchBody,
  },

  data() {
    return {
      urlFilm: 'http://www.omdbapi.com/?apikey=',
      titleAnime: 'OMDB Film Search',
    };
  },

  methods: {},
});
</script>

<style lang="scss" scoped>
.card_list_body .gambar_film {
  height: 450px;
}
</style>
