<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs"/>
    <div class="container">
      <!-- Breadcrumb -->
      <div class="row mt-3">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><router-link to="/" class="text-dark">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/foods" class="text-dark">Foods</router-link></li>
              <li class="breadcrumb-item">Cart</li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col table-responsive">
          <!-- <h2>Cart</h2> -->
          <table class="table text-center mt-3">
            <thead>
              <tr>
                <th>#</th>
                <th style="width: 15%;">Image</th>
                <th style="width: 15%;" class="text-left">Name</th>
                <th style="width: 15%;" class="text-left">Information</th>
                <th style="width: 5%;" class="text-right">Quantity</th>
                <th style="width: 20%;" class="text-right">Price</th>
                <th style="width: 20%;" class="text-right">Total</th>
                <th style="width: 10%;">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                <td>{{ index+1 }}</td>
                <td><img :src="'../assets/img/' + keranjang.products.gambar" :alt="keranjang.products.gambar" class="img-fluid shadow rounded w-100">
                </td>
                <td class="text-left">{{ keranjang.products.nama }}</td>
                <td class="text-left">{{ keranjang.keterangan ??'-' }}</td>
                <td class="text-right">{{ keranjang.jumlah_pesan }}</td>
                <td class="text-right">{{ keranjang.products.harga }}</td>
                <td class="text-right">{{ keranjang.products.harga * keranjang.jumlah_pesan }}</td>
                <td><button class="btn btn-sm btn-outline-danger" @click="hapusKeranjang(keranjang.id)"><b-icon-trash></b-icon-trash></button></td>
              </tr>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td class="text-right"><strong>Total</strong></td>
                <td class="text-right"><strong>{{ totalHarga }}</strong></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form action="" @submit.prevent>
            <div class="form-group">
              <label for="nama">Name</label>
              <input type="text" class="form-control" autofocus v-model="pesan.nama">
            </div>
            <div class="form-group">
              <label for="no_meja">Table No.</label>
              <input type="number" class="form-control" autofocus v-model="pesan.no_meja">
            </div>
            <button type="submit" class="btn btn-sm btn-outline-success float-right" @click="checkout">
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
  name: 'Keranjang',
  components: {
    Navbar
  },
  data() {
    return {
      keranjangs: [],
      pesan: {}
    }
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data
    },
    hapusKeranjang(id) {
      axios.delete('http://localhost:3000/keranjangs/'+id)
      .then(() => {
        this.$toast.success('The cart has been deleted.', {
          type: 'success', 
          position: 'top-right', 
          duration: 3000, 
          dismissable: true
        })
        
        axios.get('http://localhost:3000/keranjangs')
          .then((response) => this.setKeranjang(response.data))
          .catch((error) => console.log('error', error))
      })
      .catch((error) => console.log('error', error))
    },
    checkout() {
      if (this.pesan.nama && this.pesan.no_meja) {
        this.pesan.keranjangs = this.keranjangs

        axios.post('http://localhost:3000/pesanans', this.pesan)
          .then(() => {
            this.keranjangs.map((item) => {
              return axios.delete('http://localhost:3000/keranjangs/'+item.id)
                .then(() => {
                  axios.get('http://localhost:3000/keranjangs')
                    .then((response) => this.setKeranjang(response.data))
                    .catch((error) => console.log('error', error))
                  })
                .catch((error) => console.log('error', error))
            })

            this.$router.push({path: "/"})
            this.$toast.success('The menu will be served soon.', {
              type: 'success', 
              position: 'top-right', 
              duration: 3000, 
              dismissable: true
            })
          })
          .catch(((error) => console.log('error', error)))
      } else {
        this.$toast.error('The name and number can not be null!', {
          type: 'error', 
          position: 'top-right', 
          duration: 3000, 
          dismissable: true
        })
      }
    }
  },
  mounted() {
    axios.get('http://localhost:3000/keranjangs')
      .then((response) => this.setKeranjang(response.data))
      .catch((error) => console.log('error', error))
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items + (data.products.harga * data.jumlah_pesan)
      }, 0)
    }
  }
}
</script>

<style>

</style>