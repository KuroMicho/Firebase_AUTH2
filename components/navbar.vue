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
        <b-nav-item href="/login">Iniciar Sesion</b-nav-item>
        <b-nav-item href="/registro">Registro</b-nav-item>
        <b-nav-item href="/contacto">Contacto</b-nav-item>
        <b-nav-item href="/productos">Productos</b-nav-item>
        <b-nav-item href="/categorias">Categoria</b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
export default {};
</script>
