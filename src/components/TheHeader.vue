<template>
  <header>
    <nav>
      <router-link to="/" class="logo">
        <img src="@/assets/ranek.svg" alt="ranek logo">
      </router-link>
      <router-link class="btn" to="/usuario" v-if="$store.state.login">{{nome}}</router-link>
      <router-link class="btn" to="/login" v-else>Vender/Login</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: "TheHeader",
  data() {
    return {};
  },
  computed: {
    nome() {
      return this.$store.state.usuario.nome.replace(/ .*/, "");
    }
  }
};
</script>

<style scoped>
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
  box-shadow: 0 2px 4px rgba(30, 60, 90, 0.2);
}

.logo {
  padding: 10px 0;
}

.logo img {
  width: 90px;
}
</style>
