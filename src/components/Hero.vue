<template>
  <div class="hero">
    <!-- Desktop -->
    <div class="d-md-block d-none">
      <div class="row">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>Menu</h2>
              <p>kuliner dari kami untuk kamu.</p>
              <router-link to="/foods">
                <button class="btn btn-sm btn-outline-success">Order</button>
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/img/undraw_Eating_together_re_ux62.png" width="100%">
        </div>
      </div>
    </div>
    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row">
        <div class="col-md-6">
          <img src="../assets/img/undraw_Eating_together_re_ux62.png" width="100%">
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>Menu</h2>
              <p>kuliner dari kami untuk kamu.</p>
              <button class="btn btn-sm btn-outline-success">Order</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Hero'
}
</script>

<style>

</style>