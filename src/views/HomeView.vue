<template>
  <div class="home">
    <h1 class="title home__title"> Пакемоны </h1>
    <CatalogPage msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import CatalogPage from '@/components/CatalogPage.vue'

export default {
  name: 'HomeView',
  components: {
    CatalogPage
  }
}
</script>
