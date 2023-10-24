<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    
    <div class="wrapper">
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <RouterLink class="nav-link active" to="/" aria-current="page" href="#">Home</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/about" href="#">About Us</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/students" href="#">Students</RouterLink>
        </li>
       
      </ul>
    </div>
  </div>
</nav>
      

      
    </div>
  </header>

  <RouterView />
</template>

<style scoped>


</style>
