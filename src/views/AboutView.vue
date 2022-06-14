<!--  <img :src="'https:/apple.com/ac/structured-data/images/knowledge_graph_logo.png?202203080231'" alt="img">  -->
<template>
  <div class="container">
    <div class="about">

      <h1 class="title about__title"> {{ apiData.name }} </h1>

      <div class="about__inner">

        <div class="about__left">
          <img class="about__image" :src="imgSrc" alt="img">
        </div>

        <div class="about__right">

          <p class="about__text"> Height:
            <span class="about__text-value"> {{ apiData.height }} </span>
          </p>

          <p class="about__text"> Weight:
            <span class="about__text-value"> {{ apiData.weight }} </span>
          </p>

          <p class="about__text"> Base experience:
            <span class="about__text-value"> {{ apiData.base_experience }} </span>
          </p>

          <p class="about__text about__text_ul"> Ability: </p>
          <ul class="about__list">
            <li class="about__list-item" v-for="item of apiData.abilities">
              {{ item.ability.name }}
            </li>
          </ul>

          <p class="about__text about__text_ul"> Types: </p>
          <ul class="about__list">
            <li class="about__list-item" v-for="item of apiData.types">
              {{ item.type.name }}
            </li>
          </ul>

          <p class="about__text about__text_ul"> Stats: </p>
          <ul class="about__list">
            <li class="about__list-item" v-for="item of apiData.stats">
              {{ item.stat.name }} :
              <span class="about__list-item-value"> {{ item.base_stat }} </span>
            </li>
          </ul>

          <p class="about__text about__text_ul"> Game indices: </p>
          <ul class="about__list">
            <li class="about__list-item" v-for="item of apiData.game_indices">
              {{ item.version.name }} :
              <span class="about__list-item-value"> {{ item.game_index }} </span>
            </li>
          </ul>

          <p class="about__text about__text_ul"> Movies with this character: </p>
          <ul class="about__list">
            <li class="about__list-item" v-for="item of apiData.moves">
              {{ item.move.name }}
            </li>
          </ul>

        </div>

      </div>
      

    
    </div>
  </div>
</template>


<script>
import axios from 'axios'

export default {
  name: 'AboutView',

  props: {
    product_data: {
      type: String,
      default () {
        return ''
      }
    }
  },

  data () {
    return {
      urlApi: this.product_data,
      apiData: {},
    }
  },

  methods: {
    async getPokemonData () {
    try {
        const products=await axios.get(this.urlApi)
        // console.log(products.data)
        this.apiData = products.data
        return products.data
      } catch(error) {
        console.log(error)
        return error
      }
  }
  },

  computed: {
    imgSrc () {
      return this.apiData.sprites?.other['official-artwork']?.front_default
    }
  },

  mounted () {
    this.getPokemonData ()
  },

  
}
</script>


<style lang="scss">
  @import '../styles/style.scss';

  .about {

    &__title {
      margin-top: $mrg-big;
      text-align: center;
    }

    &__inner {
      display: flex;
      justify-content: space-between;
      margin-top: $mrg-big;
    }

    &__left, &__right {
      width: 50%;
    }

    &__image {
      margin-top: 20px;
    }

    &__text {
      margin-top: 15px;
    }

    &__text-value {
      font-size: 26px;
      margin-left: 5px;
    }

    &__text:after,
    &__list:not(:last-child):after {
      @include hr-after();
    }
    &__text_ul:after {
        display: none;
    }


    &__list {
      margin-top: 10px;
      display: flex;
      flex-wrap: wrap;
      align-items: flex-end;
      justify-content: start;
      gap: 7px 5px;
    }

    &__list-item {
      margin-left: 5px;
      font-size: 22px;
      color: yellowgreen;
      @include text-shadow($clr-blue);

      &:not(:last-child)::after {
        content: ',';
        color: $clr-white;
      }
    }

    &__list-item-value {
      margin-left: 5px;
      color: $clr-white;
    }


    @media (max-width: 768px) {
      &__inner {
        flex-direction: column;
        align-items: center;
        justify-content: center;
      }
      &__left, &__right {
        width: 100%;
      }
      &__left {
        display: flex;
        justify-content: center;
      }
      &__image {
        margin-top: 0;
      }
    }
  }

</style>

