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
      
      <!-- <pagination-block/> -->

      <div class="catalog-page__pagination">
        <div
            class="catalog-page__pagination-page"
            v-for="page in pages"
            key="page"
            :class="{'catalog-page__pagination-page_active': page === pageNumber}"
            @click="pageClick(page)"
        >
          {{ page }}
        </div>
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

    pageClick (page) {
      this.pageNumber = page
    }
  },

  computed: {
    ...mapGetters(['PRODUCTS']),

    productsFromStore () {
        return this.PRODUCTS
    },

    pages () {
      return Math.ceil (this.PRODUCTS.length / 100)
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
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
      justify-content: center;
    }

    &__pagination-page {
      margin-top: 20px;
      padding: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 18px;
      border: 0.5px solid $clr-white;
      border-radius: 5px;
      cursor: pointer;
      min-width: 30px;
      height: 30px;
      
      &:hover {
        transition: all .3s;
        background-color: $clr-blue;
      }

      &_active {
        background-color: $clr-blue;
      }
    }

  }

  





</style>