<template>
  <div class="home">
    <Navbar msg="Welcome to Your Vue.js App"/>
    <div class="container">
      <Hero></Hero>
      <div class="row mt-4">
        <div class="col-md-6">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col-md-6">
          <router-link to="/foods" class="btn btn-sm btn-outline-success float-right">Show More</router-link>
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
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct'
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    Navbar, Hero, CardProduct
  },
  data() {
    return {
      products: []
    }
  },
  methods: {
    setProducts(data) {
      this.products = data
    }
  },
  mounted() {
    axios.get('http://localhost:3000/best-products')
    .then((response) => this.setProducts(response.data))
    .catch((error) => console.log('error', error))
  }
}
</script>
