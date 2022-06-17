<template>
  <ul class="list-block">

    <li
        class="list-block__item"
        v-for="product of paginated_roducts"
        :key="product.name"
    >
      <router-link
          class="link list-block__item-link"
          :to = "{ name: 'about', params: { product_data: product.url, name: product.name } }"
      >
        {{ product.name }}
      </router-link>
    </li>

  </ul>
</template>


<script>
  export default {
    props: {
      paginated_roducts: {
        type: Array,
        default() {
          return [];
        }
      }
    }
  }
</script>


<style lang="scss">
  @import '../../styles/style.scss';

  .list-block {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 18px 8px;

    &__item {}
    &__link {}


    @media (max-width: 768px) {
      &__item {
        font-size: 20px;
      }
    }

  }

</style>