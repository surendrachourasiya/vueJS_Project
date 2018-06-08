<template>
  <header class="">
    <b-navbar toggleable="md" type="dark" variant="info">

    <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

    <b-navbar-brand href="#">NavBar</b-navbar-brand>

    <b-collapse is-nav id="nav_collapse">

      <b-navbar-nav>
        <b-nav-item ><nuxt-link to="/" class="nav-link"><a>Home</a></nuxt-link></b-nav-item>
        <b-nav-item ><nuxt-link to="/about" class="nav-link"><a>About</a></nuxt-link></b-nav-item>
        <b-nav-item ><nuxt-link to="/crud" class="nav-link"><a>Crud</a></nuxt-link></b-nav-item>
        <b-nav-item ><nuxt-link to="/add" class="nav-link"><a>Add User</a></nuxt-link></b-nav-item>
        
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto" right>
        <b-nav-item ><nuxt-link to="/login" class="nav-link">SignIn</nuxt-link></b-nav-item>
        <b-nav-item><nuxt-link to="/" class="nav-link">Signout</nuxt-link></b-nav-item>
      </b-navbar-nav>

    </b-collapse>
  </b-navbar>
  </header>
</template>

<style lang="scss">
 .nav-link a {
   text-decoration: none;
   color: white;
 }
</style>