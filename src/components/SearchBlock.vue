<template>
  <div class="search-block">
    <div class="container">

      <form class="search-block__form" action="">
        <input class="search-block__input" type="search">
        <i class="search-block__icon fa fa-search"></i>
      </form>

    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchBlock',

}
</script>


<style lang="scss">
  @import '../styles/style.scss';

  .search-block {
    display: flex;
    justify-content: right;

    &__form {
      margin-top: $mrg-big;
      margin-left: 10px;
      position: relative;
      transition: all 1s;
      width: 50px;
      height: 50px;
      background: $clr-white;
      box-sizing: border-box;
      border-radius: 25px;
      border: 4px solid $clr-white;
      padding: 5px;

      &:hover{
        width: 250px;
        cursor: pointer;
      }

      &:hover .search-block__input {
         display: block;
      }

      &:hover .fa{
        background: $clr-dark;
        color: $clr-white;
      }
    }

    &__input {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 42.5px;
      line-height: 30px;
      outline: 0;
      border: 0;
      display: none;
      border-radius: 20px;
      padding: 0 20px;
    }

    &__icon {
      box-sizing: border-box;
      padding: 10px;
      width: 42.5px;
      height: 42.5px;
      position: absolute;
      top: 0;
      right: 0;
      border-radius: 50%;
      color: $clr-dark;
      text-align: center;
      font-size: 1.1em;
      transition: all 1s;
    }
  }



</style>

