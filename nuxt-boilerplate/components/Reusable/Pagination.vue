<template>
  <div class="justify-center items-center text-center">
    <div v-if="maxPage > 1" class="pagination">
      <!-- previous page -->
      <!-- <a v-if="currentPage === 1" disabled>&laquo;</a> -->
      <a
        v-if="currentPage > 1"
        class="next_previous hover:ring-2 hover:ring-yellow-900"
        @click.prevent="onChangePage(currentPage - 1)"
        >&laquo;</a
      >

      <!-- pagination numbber -->
      <a
        v-if="elipsisStart"
        aria-label="Goto page 1"
        @click.prevent="onChangePage(1)"
        >1</a
      >
      <a v-if="elipsisStart" @click.prevent="onChangePage(1)">&hellip;</a>
      <a
        v-for="(page, index) in pages"
        :key="index"
        aria-label="'Goto page'+ page"
        :class="{ active: page === currentPage }"
        @click.prevent="onChangePage(page)"
        >{{ page }}</a
      >
      <a v-if="elipsisEnd" aria-label="Goto page hellp">&hellip;</a>
      <a
        v-if="elipsisEnd"
        :aria-label="'Goto page'"
        @click.prevent="onChangePage(maxPage)"
        >{{ maxPage }}</a
      >

      <!-- next page -->
      <!-- <a v-if="currentPage >= maxPage" disabled>&raquo;</a> -->
      <a
        v-if="currentPage < maxPage"
        class="next_previous hover:ring-2 hover:ring-yellow-900"
        @click.prevent="onChangePage(currentPage + 1)"
        >&raquo;</a
      >
    </div>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';

declare interface Player {
  pages: Number[];
}

export default Vue.extend({
  props: {
    maxPage: {
      type: Number,
      default: 0,
    },
  },

  data() {
    return {
      currentPage: 1,
      maxPagination: 3,
      elipsisStart: false,
      elipsisEnd: false,
      minFilm: 0,
      maxFilm: 9,
      pages: [] as Number[],
    };
  },

  mounted() {
    this.updateElipsis();
  },

  methods: {
    makePages(startFrom: number, length: number): Number[] {
      const pages = [];
      for (let i = 0; i < length; i++) {
        pages.push(startFrom + i);
      }
      return pages;
    },

    startEndFilm() {
      this.maxFilm = 9 * this.currentPage;
      this.minFilm = this.maxFilm - 9;
      this.$emit('changePage', this.minFilm, this.maxFilm);
    },

    updateElipsis() {
      // data hanya 1
      if (this.maxPage <= this.maxPagination) {
        this.elipsisStart = false;
        this.elipsisEnd = false;
        this.pages = this.makePages(1, this.maxPage);
        this.startEndFilm();
      }
      // permulaan (nomor awal)
      else if (this.currentPage <= 2) {
        this.elipsisStart = false;
        this.elipsisEnd = true;
        this.pages = this.makePages(1, this.maxPagination);
        this.startEndFilm();
      }

      // nomor akhir
      else if (this.currentPage >= this.maxPage - 1) {
        this.elipsisStart = true;
        this.elipsisEnd = false;
        this.pages = this.makePages(
          this.maxPage - this.maxPagination + 1,
          this.maxPagination
        );
        this.startEndFilm();
      }

      // choice nomor
      else {
        this.elipsisStart = true;
        this.elipsisEnd = true;
        this.pages = this.makePages(this.currentPage - 1, this.maxPagination);
        this.startEndFilm();
      }
    },

    onChangePage(page: number) {
      this.currentPage = page;
      this.updateElipsis();
    },
  },
});
</script>

<style lang="scss" scoped>
.pagination {
  display: inline-block;
}

.pagination a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
}

.pagination a.active {
  background-color: #4caf50;
  color: white;
}

.pagination a:hover:not(.active) {
  background-color: #ddd;
}

.pagination a:hover:not(.active).next_previous {
  background-color: #fcd34d;
}
</style>
