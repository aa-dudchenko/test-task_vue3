<template>
  <div class="catalog-page">
    <div class="container">

      <h1 class="title catalog-page__title"> Pokemons: </h1>

      <ul class="catalog-page__list">
        <li 
        class="catalog-page__list-item"
        v-for="product of paginatedProducts"
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

      <div class="catalog-page__pagination">
         <pagination-block
          :pages = "pages"
          :pageNumber = "pageNumber"
          @changedPageNumber = "pageNumber = $event"
         />
      </div>

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
      productPerPage: 100,
      pageNumber: 1
    }
  },

  methods: {
    ...mapActions(['GET_PRODUCTS_FROM_API',]),
  },

  computed: {
    ...mapGetters(['PRODUCTS']),

    pages () {
      return Math.ceil (this.PRODUCTS.length / this.productPerPage)
    },

    paginatedProducts () {
      let from = (this.pageNumber - 1) * this.productPerPage
      let to = from + this.productPerPage
      return this.PRODUCTS.slice( from, to )
    }
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

    &__pagination {
      margin-top: $mrg-big;
    }


    @media (max-width: 768px) {

      &__list-item {
         font-size: 20px;
      }
    }

  }

  





</style>