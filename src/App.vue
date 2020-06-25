<template>
  <div>
    <table>
      <thead>
        <tr>
          <td>Nome</td>
          <td>Descrição</td>
          <td>Valor</td>
          <td>Desconto</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="produto in produtos" :key="produto._id">
          <td>{{ produto.nome }}</td>
          <td>{{ produto.descricao }}</td>
          <td>R${{ produto.valor }}</td>
          <td>{{ produto.desconto }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
      produtos: null
    }
  },
  mounted(){
    this.getProdutos();
  },
  methods: {
    getProdutos(){
      axios
        .get('https://server-node-example.herokuapp.com/produtos')
          .then( response => {
            console.log(response)
            this.produtos = response.data
          })
          .catch( e=> console.log(e) )
    }
  }
}

</script>

<style>
thead tr {
  font-weight: bold;
}
</style>
