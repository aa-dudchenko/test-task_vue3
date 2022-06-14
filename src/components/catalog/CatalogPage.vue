<template>
  <div class="catalog-page">
    <div class="container">

      <h1 class="title catalog-page__title"> Pokemons: </h1>

      <ul class="catalog-page__list">
        <li 
        class="catalog-page__list-item"
        v-for="product of productsFromStore"
        :key="product.name" 
        > 
        <router-link
          class="link catalog-page__item-link"
          :to = "{ name: 'about', params: { product_data: product.url, name: product.name } }"
        > 
          {{ product.name }} 
        </router-link>
        </li>
      </ul>
      
      <!-- <pagination-block/> -->

    </div>
  </div>
    
</template>

<script>
import PaginationBlock from '@/components/catalog/PaginationBlock.vue'
import { mapGetters,  mapActions } from 'vuex'

export default {
  name: 'CatalogPage',
  data () {
    return {
     forExample: 'data from catalogPage'
    }
  },

  methods: {
    ...mapActions(['GET_PRODUCTS_FROM_API',]),
  },

  computed: {
    ...mapGetters(['PRODUCTS']),

    productsFromStore () {
        return this.PRODUCTS
    },
  },

  mounted () {

    this.GET_PRODUCTS_FROM_API()
    .then( response => { 
      if(response) {
        console.log('DATA RECEIVED')
      } else { console.log('DATA WAS NOT RECEIVED') }
     })
  },

  components: {
    PaginationBlock
  }
  
}
</script>


<style lang="scss">
  @import '../../styles/style.scss';

  .catalog-page {

    &__title {
      margin-top: $mrg-big;
    }

    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 18px 8px;
      margin-top: $mrg-mini;
    }

    &__list-item {}
    &__item-link {}

  }

  





</style>