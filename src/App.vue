<template>
  <div>
    <b-card-grouo columns>
      <b-card v-for="produto in produtos" v-bind:key="produto._id" v-bind:title="produto.nome">
        <b-card-text>{{ produto.descricao }}</b-card-text>
        <div v-if="produto.desconto == ''">
          <b-card-text>R${{ produto.valor }}</b-card-text>
        </div>
        <div v-else>
          <b-card-text>De: <span id="valorAntigo">R${{ produto.valor }}</span></b-card-text>
          <b-card-text>Por: R${{ produto.valor }}</b-card-text>
        </div>
      </b-card>
    </b-card-grouo>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      produtos: null
    };
  },
  mounted() {
    this.getProdutos();
  },
  methods: {
    getProdutos() {
      axios
        .get("https://server-node-example.herokuapp.com/produtos")
        .then(response => {
          console.log(response.data);
          this.produtos = response.data;
        })
        .catch(e => console.log(e));
    }
  }
};
</script>

<style>
thead tr {
  font-weight: bold;
}
#valorAntigo {
  text-decoration: line-through;
}
</style>
