<template>
  <div id="app">
    <ul>
      <li
        is="product-elem"
        v-for="product in products"
        v-bind:item="product"
      ></li>
    </ul>
  </div>
</template>

<script>
import ProductElem from "./components/productElem";
import products from "./products"
export default {
  mounted(){
     this.products=products;
  },
  name: 'app',
  components: {ProductElem},
  data () {
    return {
      products:[],
    }
  }
}
</script>

<style lang="scss">
ul{
  list-style-type:none;
}
</style>
