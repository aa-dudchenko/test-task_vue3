<template>
  <div class="home">
    
    <h1 class="home__title"> Pokemons- info </h1>

    <search-block/>
    <catalog-page/>

  </div>
</template>

<script>

import CatalogPage from '@/components/catalog/CatalogPage.vue'
import SearchBlock from '@/components/SearchBlock.vue'


export default {
  name: 'HomeView',

  components: {
    CatalogPage,
    SearchBlock,
  }
}
</script>


<style lang="scss">
  @import '../styles/style.scss';
  
  .home {
    
    &__title {
      color: $clr-dark;
      text-align: center;
      margin-top: $mrg-mini;
      font-size: 50px;
      @include text-shadow($clr-white)
    }
  }


</style>
