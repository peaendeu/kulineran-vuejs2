<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <!-- <a class="navbar-brand" href="/">Kulineran</a> -->
      <router-link class="nav-brand navnav" to="/">Kulineran</router-link>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <!-- <div class="navbar-nav">
          <router-link class="nav-link" to="/">Home</router-link>
        </div> -->
        <div class="navbar-nav">
          <router-link class="nav-link" to="/foods">Foods</router-link>
        </div>
        <div class="navbar-nav ml-auto">
          <router-link class="nav-link" to="/cart">
            <!-- Cart -->
            <b-icon-bag></b-icon-bag>
            <span class="badge badge-success ml-2">0</span>
          </router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style>

</style>