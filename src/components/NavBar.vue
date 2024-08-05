<template>
  <b-navbar toggleable="lg" type="light" variant="light" class="custom-navbar">
    <b-navbar-brand href="#">
      <img src="@/assets/vegetales.png" class="navbar-image">
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#">Productos</b-nav-item>
        <b-nav-item href="#">Stock</b-nav-item>
      </b-navbar-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown right>
          <template #button-content>
            <img src="@/assets/avatar.svg" class="user-image" alt="Configuración">
          </template>
          <b-dropdown-item href="#">Perfil</b-dropdown-item>
          <b-dropdown-item href="#">cerrar sesion</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
import Vue from 'vue';
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap-vue/dist/bootstrap-vue.css';
import '@/assets/sass/custom.scss';

Vue.use(BootstrapVue);
Vue.use(IconsPlugin);

export default {
  name: "NavBar"
}
</script>

<style scoped>
.navbar-image {
  max-height: 70px;
  border-radius: 20px
}

.user-image {
  max-height: 40px;
  border-radius: 50%;
}
</style>
