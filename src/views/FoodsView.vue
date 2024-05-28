<template>
  <div>
    <Navbar></Navbar>
    <div class="container">
      <div class="row mt-3">
        <div class="col">
          <h2>Food List</h2>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col input-group mb-3">
          <input type="text" class="form-control" autofocus v-model="search" @keyup="searchFood">
          <div class="input-group-append">
            <button class="btn btn-success" type="button" id="button-addon2"><b-icon-search></b-icon-search></button>
          </div>
        </div>
      </div>
      <div class="row mb-5">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product"></CardProduct>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import CardProduct from '@/components/CardProduct'
import axios from 'axios'

export default {
  name: 'FoodsView',
  components: {
    Navbar, CardProduct
  },
  data() {
    return {
      products: [],
      search: [],
    }
  },
  methods: {
    setProducts(data) {
      this.products = data
    },
    searchFood() {
      axios.get('http://localhost:3000/products?q=' + this.search)
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log('error', error))
    },
  },
  mounted() {
    axios.get('http://localhost:3000/products')
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log('error', error))
  }
}
</script>

<style>

</style>