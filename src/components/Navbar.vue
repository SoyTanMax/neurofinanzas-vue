<template>
    <nav class="navbar is-transparent">
      <div class="navbar-brand">
          <div class="navbar-item">
            <router-link :to="{name: 'Home'}">
                <img class="image" src="@/assets/logo-nf-blanco.svg"/>
            </router-link>
          </div>
        <!--
    Using the v-on: directive to listen for the click event and toggle the data property showNav. Also, using the v-bind: directive to reactively update the class attribute 'is-active' based on the showNav property.
    -->
        <div class="navbar-burger" @click="showNav = !showNav" :class="{ 'is-active': showNav }">
          <span class="has-text-white"></span>
          <span class="has-text-white"></span>
          <span class="has-text-white"></span>
        </div>
      </div>
      <!--
    Using the v-bind: directive to reactively update the class attribute 'is-active' based on the showNav property.
    -->
      <div class="navbar-menu" :class="{ 'is-active': showNav }">
        <div class="navbar-end">
            <ul class="navbar-item">
                <a href="https://www.facebook.com/neurofinanzasac/">
                    <li>
                        <i class="is-size-5 fab fa-facebook"></i>
                    </li>
                </a>
                <a href="https://www.instagram.com/neurofinanzasac/">
                    <li>
                        <i class="is-size-5 fab fa-instagram"></i>
                    </li>
                </a>
                <a href="https://twitter.com/Neurofinanzas1">
                    <li>
                        <i class="is-size-5 fab fa-twitter"></i>
                    </li>
                </a>
            </ul>
        </div>
      </div>
    </nav>
</template>

<script>
    export default {
        name: 'Navbar',
        data() {
            return {
                showNav: false
            }
        },
    }
</script>

<style scoped>
nav {
    padding-top: 16px;
    width: 90%;
    margin: 0 auto;
}
li {
    padding: 10px;
}
/* mobile */
@media screen and (max-width: 769px) {
  nav {
    width: 100%;
    position: relative;
  }
  .navbar-menu{
      position: fixed;
      width: 100%;
      height: 100vh;
  }
  li {
      color: #000000;
  }
}
</style>