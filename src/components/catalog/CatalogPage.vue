<template>
  <div class="catalog-page">
    <div class="container">

      <h2 class="title catalog-page__title"> Pokemon names: </h2>
      <ul class="list catalog-page__list">
        <li 
        class="list__item"
        v-for="product of productsFromStore"
        :key="product.name" 
        > 

        <a href="#" class="list__item-link" >
          {{ product.name }} 
        </a>

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
      margin-top: $mrg-mini;
    }

   
  }

  





</style>