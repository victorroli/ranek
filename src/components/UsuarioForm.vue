<template>
  <form>
    <div class="usuario" v-if="mostraDadosLogin">
      <label for="nome">Nome:</label>
      <input id="nome" type="text" name="nome" v-model="nome">

      <label for="email">Email:</label>
      <input id="email" type="email" name="email" v-model="email">

      <label for="senha">Senha:</label>
      <input id="senha" type="password" name="senha" v-model="senha">
    </div>

    <label for="cep">Cep</label>
    <input id="cep" type="text" name="cep" v-model="cep" @keyup="preencherCep" maxlength="8">

    <label for="rua">Rua</label>
    <input id="rua" type="text" name="rua" v-model="rua">

    <label for="numero">Número</label>
    <input id="numero" type="text" name="numero" v-model="numero">

    <label for="bairro">Bairro</label>
    <input id="bairro" type="text" name="bairro" v-model="bairro">

    <label for="cidade">Cidade</label>
    <input id="cidade" type="text" name="cidade" v-model="cidade">

    <label for="estado">Estado</label>
    <input id="estado" type="text" name="estado" v-model="estado">

    <div class="button">
      <slot></slot>
    </div>
  </form>
</template>

<script>
import { mapFields } from "@/helpers.js";
import { getCep } from "@/services.js";

export default {
  name: "UsuarioForm",
  computed: {
    ...mapFields({
      fields: [
        "nome",
        "email",
        "senha",
        "rua",
        "cep",
        "numero",
        "bairro",
        "cidade",
        "estado"
      ],
      base: "usuario",
      mutation: "UPDATE_USUARIO"
    }),
    mostraDadosLogin() {
      return !this.$store.state.login || this.$route.name === "usuario-editar";
    }
  },
  methods: {
    preencherCep() {
      const cep = this.cep.replace(/\D/g, "");
      if (cep.length == 8) {
        getCep(cep).then(response => {
          this.rua = response.data.logradouro;
          this.bairro = response.data.bairro;
          this.estado = response.data.uf;
          this.cidade = response.data.localidade;
        });
      }
    }
  }
};
</script>

<style scoped>
form,
.usuario {
  display: grid;
  grid-template-columns: 80px 1fr;
  align-items: center;
}

.usuario {
  grid-column: 1/ 3;
}

.button {
  grid-column: 2;
  margin-top: 15px;
}
</style>
