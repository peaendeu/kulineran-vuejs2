<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <router-link to="/" style="font-weight: bold;">Kulineran</router-link>
    
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
    
        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </b-navbar-nav>
    
          <b-navbar-nav class="ml-auto">
            <router-link class="nav-link" to="/cart">
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2">{{ updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length }}</span>
            </router-link>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Navbar',
  data() {
    return {
      jumlah_pesanan: []
    }
  },
  props: ['updateKeranjang'],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanan = data
    }
  },
  mounted() {
    axios.get('http://localhost:3000/keranjangs/')
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log('error', error))
  }
}
</script>

<style>

</style>