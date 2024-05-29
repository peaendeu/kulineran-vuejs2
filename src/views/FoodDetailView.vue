<template>
  <div class="food-detail">
    <Navbar></Navbar>
    <div class="container">
      <!-- Breadcrumb -->
      <div class="row mt-3">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><router-link to="/" class="text-dark">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/foods" class="text-dark">Foods</router-link></li>
              <li class="breadcrumb-item">Order</li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt3">
        <div class="col-md-6">
          <img :src="'../assets/img/' + product.gambar" :alt="product.gambar" class="img-fluid shadow rounded">
          <!-- <img :src=" 'assets/img/' + product.gambar " :alt="product.gambar"> -->
        </div>
        <div class="col-md-6">
          <h2><strong>{{ product.nama }}</strong></h2>
          <h4>Rp. {{ product.harga }},-</h4>
          <form action="" @submit.prevent>
            <div class="form-group">
              <label for="jumlah_pesan">Quantity</label>
              <input type="number" class="form-control" placeholder="1 2 3 4 5" autofocus v-model="pesan.jumlah_pesan">
            </div>
            <div class="form-group">
              <label for="keterangan">Information</label>
              <textarea type="text" class="form-control" placeholder="Very spicy, don't be too salty or no vegetables." v-model="pesan.keterangan"></textarea>
            </div>
            <button type="submit" class="btn btn-sm btn-outline-success float-right" @click="pemesanan">
              <b-icon-cart></b-icon-cart>
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import axios from 'axios'

export default {
  name: 'FoodDetailView',
  components: {
    Navbar
  },
  data() {
    return {
      product: {},
      pesan: {}
    }
  },
  methods: {
    setProduct(data) {
      this.product = data
    },
    pemesanan() {
      if (this.pesan.jumlah_pesan) {
        this.pesan.products = this.product
        axios.post('http://localhost:3000/keranjangs', this.pesan)
          .then(() => {
            this.$router.push({path: "/keranjang"})
            this.$toast.success('Menu has been added to cart.', {
              type: 'success', 
              position: 'top-right', 
              duration: 3000, 
              dismissable: true
            })
          })
          .catch(((error) => console.log('error', error)))
      } else {
        this.$toast.error('The quantity can\'t be empty!', {
          type: 'error', 
          position: 'top-right', 
          duration: 3000, 
          dismissable: true
        })
      }
    }
  },
  mounted() {
    axios.get('http://localhost:3000/products/' + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log('error', error))
  }
}
</script>

<style>

</style>