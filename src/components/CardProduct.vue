<template>
  <div>
    <div class="card shadow" style="border-radius: 15px;">
      <!-- <img src="../assets/img/bakso.jpg" width="100%" style="border-top-left-radius: 15px; border-top-right-radius: 15px;"> -->
      <img :src=" 'assets/img/' + product.gambar " class="card-img-top" :alt="product.gambar" style="border-top-left-radius: 15px; border-top-right-radius: 15px;">
      <div class="card-body">
        <h5 class="card-title">{{ product.nama }}</h5>
        <p class="card-text">{{ product.harga }}</p>
        <router-link class="btn btn-sm btn-outline-success" :to="'/foods/' + product.id"><b-icon-cart></b-icon-cart></router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProduct',
  props: ['product']
}
</script>

<style>

</style>