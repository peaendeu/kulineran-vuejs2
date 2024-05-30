<template>
  <div class="pesanan-sukses">
    <Navbar></Navbar>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col text-center">
          <img src="../assets/img/menunggu.png" alt="menunggu.png" width="25%">
          <h2>Be patient please,</h2>
          <h4>The menu will be served soon.</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
export default {
  name: 'PesananSukses',
  components: {
    Navbar
  },
}
</script>

<style>

</style>