<template>
  <!-- seacrh film input -->
  <section class="SearchInput text-black">
    <h2 class="text-black mb-5 text-3xl font-semibold">{{ titleFilmAnime }}</h2>
    <div class="justify-center flex items-center">
      <input
        v-model="searchFilmOn"
        placeholder="Search Film..."
        type="text"
        class="text-black border w-1/3 border-transparent focus:outline-none focus:ring-2 focus:ring-yellow-400 focus:border-transparent shadow-lg py-2 px-3 rounded-md"
        @keyup.enter="searchFilm()"
      />
      <button
        :class="{
          'bg-yellow-200': !searchFilmOn,
          'bg-yellow-400': searchFilmOn,
          'text-gray-100': !searchFilmOn,
        }"
        class="submit shadow-lg focus:outline-none focus:ring-2 focus:ring-yellow-600 focus:ring-opacity-50 rounded-md py-2 px-4 ml-4"
        type="submit"
        :disabled="!searchFilmOn"
        @click="searchFilm()"
      >
        Search
      </button>
    </div>

    <!-- Card List -->
    <div class="block">
      <div class="justify-center items-center text-center">
        <div v-if="loadingCondition" class="block">
          <loading></loading>
        </div>

        <p
          v-else-if="!loadingCondition && responseData === 'False'"
          class="block font-black mt-10"
        >
          No Result Film
        </p>

        <p v-else-if="errorMessage" class="block">{{ errorMessage }}</p>

        <div
          v-else-if="
            !loadingCondition &&
            dataFilmOn.length > 1 &&
            responseData === 'True'
          "
          class="card_list_body flex grid grid-cols-3 pt-12 pb-4"
        >
          <div
            v-for="(itemFilm, index) in dataFilmOn.slice(minFilmOn, maxFilmOn)"
            :key="index"
            class="shadow-lg rounded-md bg-gray-50 mr-10 mb-10 text-left"
          >
            <!--anime  -->
            <div v-if="urlFilmAnime === 'Anime'">
              <div class="frame_gambar bg-transparent">
                <img
                  class="gambar_film w-full rounded-md"
                  :src="itemFilm.image_url"
                  :alt="itemFilm.title"
                />
              </div>

              <div class="px-8 py-4 text-gray-400">
                <h4 class="text-gray-700 mb-2 text-center">
                  {{ itemFilm.title }}
                </h4>
                <ul class="list-disc ml-10 mb-4">
                  <li type="date">Tahun: {{ itemFilm.start_date }}</li>
                  <li>Type: {{ itemFilm.type }}</li>
                  <li>Episode: {{ itemFilm.episodes }}</li>
                </ul>
                <button
                  class="submit text-white bg-yellow-400 focus:outline-none focus:ring-2 focus:ring-blue-600 focus:ring-opacity-50 rounded-md py-2 px-4"
                  type="submit"
                >
                  Show Details
                </button>
              </div>
            </div>

            <!-- film -->
            <div v-else>
              <img
                class="w-full rounded-md"
                :src="itemFilm.Poster"
                :alt="itemFilm.Title"
              />
              <div class="px-8 py-4 text-gray-400">
                <h4 class="text-gray-700 mb-2">{{ itemFilm.Title }}</h4>
                <ul class="list-disc ml-10 mb-4">
                  <li>Tahun: {{ itemFilm.Year }}</li>
                  <li>Type: {{ itemFilm.Type }}</li>
                </ul>
                <button
                  class="submit text-white bg-yellow-400 focus:outline-none focus:ring-2 focus:ring-blue-600 focus:ring-opacity-50 rounded-md py-2 px-4"
                  type="submit"
                >
                  Show Details
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Pagination -->
    <pagination
      v-if="maxPage > 1"
      :max-page="maxPage"
      @changePage="changepagination"
    >
    </pagination>
  </section>
</template>

<script lang="ts">
import Vue from 'vue';
import Loading from '../Utilis/Loading.vue';
import Pagination from './Pagination.vue';
export default Vue.extend({
  components: {
    Loading,
    Pagination,
  },
  props: {
    urlFilmAnime: {
      type: String,
      default: 'Film',
    },
    titleFilmAnime: {
      type: String,
      default: '',
    },
  },

  data() {
    return {
      dataFilmOn: [],
      selectFilmAnimeOn: '',
      searchFilmOn: '',
      loadingCondition: false,
      responseData: '',
      errorMessage: '',
      maxPage: 0 as Number,
      minFilmOn: 0 as Number,
      maxFilmOn: 9 as Number,
    };
  },

  mounted() {
    this.urlChoiceAnimeFilm();
  },

  methods: {
    urlChoiceAnimeFilm() {
      if (this.urlFilmAnime === 'Anime') {
        this.selectFilmAnimeOn = 'https://api.jikan.moe/v3/search/anime?q=';
      } else {
        this.selectFilmAnimeOn = 'http://www.omdbapi.com/?apikey=3e60dd3&s=';
      }
    },

    searchFilm() {
      this.loadingCondition = true;
      const dataFilm = fetch(this.selectFilmAnimeOn + this.searchFilmOn, {})
        .then((response) => {
          //   console.log('data');
          this.loadingCondition = false;
          if (response.ok) {
            return response.json();
          } else {
            throw new Error('could not reach data');
          }
        })
        .then((user) => {
          return user;
        })
        .catch((error) => {
          //   console.error(error);
          this.loadingCondition = false;
          this.errorMessage = error.message;
        });

      // async await
      const printDataFilm = async () => {
        const dataFilmReady = await dataFilm;

        if (this.urlFilmAnime === 'Anime') {
          this.responseData = 'True';
          this.dataFilmOn = dataFilmReady.results;
          this.maxPage = Math.ceil(this.dataFilmOn.length / 9);
        } else {
          this.responseData = dataFilmReady.Response;
          this.dataFilmOn = dataFilmReady.Search;
          this.maxPage = Math.ceil(this.dataFilmOn.length / 9);
        }
      };
      printDataFilm();

      this.searchFilmOn = '';
    },

    changepagination(minFilm: number, maxFilm: number) {
      this.minFilmOn = minFilm;
      this.maxFilmOn = maxFilm;
    },
  },
});
</script>

<style lang="scss" scoped>
.card_list_body .frame_gambar {
  z-index: 1;
  height: 450px;
  img.gambar_film {
    z-index: 5;
    max-height: 450px;
  }
}
</style>
