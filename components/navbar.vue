<template>
  <b-navbar variant="dark" type="dark" toggleable="lg">
    <b-navbar-brand class="c5e-logo-lockup" href="/">
      <img
        class="c5e-logo-lockup-icon"
        fb-logo
        fb-size="28"
        alt
        src="https://firebasestorage.googleapis.com/v0/b/nuxt-7dafb.appspot.com/o/JVinLogo.png?alt=media&token=cd7a41fd-aaa8-42c5-9a0e-b0853b3e89f8"
        role="presentation"
      >
    </b-navbar-brand>
    <b-navbar-toggle target="menu"/>

    <b-collapse is-nav id="menu">
      <b-navbar-nav>
        <b-nav-item href="/contacto">Contacto</b-nav-item>
        <b-nav-item href="/productos" v-if="user">Productos</b-nav-item>
        <b-nav-item href="/categorias" v-if="user">Categoria</b-nav-item>
      </b-navbar-nav>

      <b-navbar-nav class="ml-auto">
        <b-nav-item href="/login" v-if="!user">Iniciar Sesion</b-nav-item>
        <b-nav-item href="/registro" v-if="!user">Registro</b-nav-item>
        <img :src="avatar" v-if="avatar" width="80px" height="80px">
        <h1 v-else></h1>
      </b-navbar-nav>

      <b-dropdown :text="name" variant="outline-danger" class="m-md-3" v-if="user">
        <b-dropdown-item @click="cerrar()">Salir</b-dropdown-item>
      </b-dropdown>
    </b-collapse>
  </b-navbar>
</template>

<script>
import { auth } from "../services/firebase";
export default {
  data() {
    return {
      user: false,
      avatar: false
    };
  },

  created() {
    auth.onAuthStateChanged(user => {
      this.user = user;
      this.name = user.displayName;
      this.avatar = user.photoURL;
    });
  },
  methods: {
    cerrar() {
      auth
        .signOut()
        .then(function() {
          this.$router.push({ path: "/" });
        })
        .catch(function(error) {
          // An error happened.
        });
    }
  }
};
</script>

