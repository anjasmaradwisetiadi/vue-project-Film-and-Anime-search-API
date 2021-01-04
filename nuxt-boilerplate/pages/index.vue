<template>
  <div>
    <!-- <Navbar /> -->
    <!-- <page-anime-list></page-anime-list> -->
    <!-- <page-film-list> </page-film-list> -->
    <Main />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'nuxt-class-component';

@Component
export default class IndexPage extends Vue {}
</script>

<style lang="scss">
.container {
  @apply mx-auto my-0 min-h-screen flex justify-center items-center text-center;
}

.links,
.title {
  @apply mt-5;
}

.links :not(:first-child) {
  @apply ml-5;
}
</style>
