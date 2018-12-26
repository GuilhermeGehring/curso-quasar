<template>
  <q-page padding>
    <h5>Detalhes do Produtos</h5>

    <table class="q-table q-table-horizontal-separator">
      <tbody>
        <tr>
          <th>id</th>
          <td>{{ product.id }}</td>
        </tr>
        <tr>
          <th>Título</th>
          <td>{{ product.title }}</td>
        </tr>
        <tr>
          <th>Preço</th>
          <td>{{ product.price }}</td>
        </tr>
      </tbody>
    </table>
    <q-btn color="negative" @click="deleteConfirm = !deleteConfirm">Remover</q-btn>
    <q-modal content-css="padding: 0 30px 30px 30px;" v-model="deleteConfirm">
      <h5>Deseja remover o seguinte produto?</h5>
      <q-btn color="positive" @click="deleteConfirm = false">Não</q-btn>
      <q-btn color="negative" @click.native="remove()">Sim</q-btn>
    </q-modal>
  </q-page>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      product: {},
      deleteConfirm: false
    }
  },
  methods: {
    remove () {
      axios.delete('http://localhost:8765/api/products/' + this.$route.params.id + '.json')
        .then((response) => this.$router.push('/products'))
    }
  },
  mounted () {
    axios.get('http://localhost:8765/api/products/' + this.$route.params.id + '.json')
      .then((response) => { this.product = response.data.product })
  }
}
</script>

<style>
  .layout-padding h5 {
    margin-top: 0px;
  }
</style>
