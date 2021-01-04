<template>
  <section class="bg-black-500 text-white justify-center md:mx-0">
    <Navbar />
    <div class="w-full px-28 py-8">
      <search-body :url-film-anime="urlAnime" :title-film-anime="titleAnime">
      </search-body>
    </div>
    <Footer />
  </section>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      urlAnime: 'Anime',
      titleAnime: 'JIKAN Anime Search',
    };
  },
});
</script>

<style lang="scss" scoped>
.card_list_body .gambar_film {
  height: 450px;
}
</style>
