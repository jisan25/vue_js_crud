<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>

  <div class="wrapper">

      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container">
              <RouterLink class="navbar-brand" to="#">Vue JS Crud</RouterLink>
              <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
              </button>
              <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                <div class="navbar-nav">
                  <RouterLink class="nav-link active" aria-current="page" to="/">Home</RouterLink>
                  <RouterLink class="nav-link" to="/about">About</RouterLink>
                  <RouterLink class="nav-link" to="/students">Students</RouterLink>
                
                </div>
              </div>
            </div>
    </nav>
</div>
     
  </header>

  <RouterView />
</template>

<style scoped>

</style>
