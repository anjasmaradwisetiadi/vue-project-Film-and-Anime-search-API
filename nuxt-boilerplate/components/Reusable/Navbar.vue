<template>
  <nav class="flex justify-between flex-wrap bg-gray-500 p-4">
    <div class="flex">
      <h2 class="text-white mx-4 pr-14" href="">
        <nuxt-link to="/">OMDB Film </nuxt-link>
      </h2>
    </div>
    <div class="block md:hidden">
      <button
        class="border border-white py-2 px-3 rounded text-white hover:bg-gray-400"
        @click="toggle()"
      >
        <svg
          id="light"
          enable-background="new 0 0 24 24"
          height="24"
          viewBox="0 0 24 24"
          width="24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <g>
            <path
              d="m21.5 24h-19c-1.379 0-2.5-1.122-2.5-2.5v-19c0-1.378 1.121-2.5 2.5-2.5h19c1.379 0 2.5 1.122 2.5 2.5v19c0 1.378-1.121 2.5-2.5 2.5zm-19-23c-.827 0-1.5.673-1.5 1.5v19c0 .827.673 1.5 1.5 1.5h19c.827 0 1.5-.673 1.5-1.5v-19c0-.827-.673-1.5-1.5-1.5z"
            />
          </g>
          <g>
            <path
              d="m16.5 8h-9c-.276 0-.5-.224-.5-.5s.224-.5.5-.5h9c.276 0 .5.224.5.5s-.224.5-.5.5z"
            />
          </g>
          <g>
            <path
              d="m16.5 12.5h-9c-.276 0-.5-.224-.5-.5s.224-.5.5-.5h9c.276 0 .5.224.5.5s-.224.5-.5.5z"
            />
          </g>
          <g>
            <path
              d="m16.5 17h-9c-.276 0-.5-.224-.5-.5s.224-.5.5-.5h9c.276 0 .5.224.5.5s-.224.5-.5.5z"
            />
          </g>
        </svg>
        <title>Menu</title>
      </button>
    </div>

    <div
      :class="open ? 'block' : 'hidden'"
      class="w-full block flex-grow md:flex md:w-auto py-2"
    >
      <div class="md:flex-grow">
        <a
          class="block md:inline-block text-gray-300 mt-2 md:mt-0 hover:text-white hover:underline mr-6"
        >
          <nuxt-link to="/PageFilmList"> Film List </nuxt-link>
        </a>
        <a
          class="block md:inline-block text-gray-300 mt-2 md:mt-0 hover:text-white hover:underline mr-6"
        >
          <nuxt-link to="/PageAnimeList">Anime List </nuxt-link>
        </a>
        <a
          class="block md:inline-block text-gray-300 mt-2 md:mt-0 hover:text-white hover:underline"
        >
          <nuxt-link to="/RouteCoba">Search </nuxt-link></a
        >
      </div>
      <div>
        <a
          class="block md:inline-block text-gray-300 mt-2 md:mt-0 hover:text-white mr-6 hover:underline mr-6"
          >Register</a
        >
        <a
          class="block md:inline-block text-gray-300 mt-2 md:mt-0 hover:text-white hover:underline mr-6"
          >Login</a
        >
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  data() {
    return {
      open: false,
    };
  },
  methods: {
    toggle() {
      this.open = !this.open;
    },
  },
});
</script>

<style lang="scss" scoped></style>
