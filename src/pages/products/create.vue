<template>
  <q-page padding>
    <h5>Novo estoque</h5>

    <form>
      <q-field label="Título">
        <q-input v-model="data.title"/>
      </q-field>
      <q-field label="Preço">
        <q-input v-model="data.price"/>
      </q-field>
      <q-field label="Custo">
        <q-input v-model="data.cost"/>
      </q-field>
      <q-field label="Descrição">
        <q-input
          type="textarea"
          v-model="data.description"
        />
      </q-field>
      <q-field label="Alerta de Quantidade">
        <q-input v-model="data.alert_quantity"/>
      </q-field>

      <q-btn color="primary" @click="save()">Salvar</q-btn>
    </form>
  </q-page>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      data: {
        status: 1
      }
    }
  },
  methods: {
    save () {
      const qs = require('qs')
      let data = qs.stringify(this.data)
      axios.post('http://localhost:8765/api/products.json', data).then(() => {
        this.$router.push('/products')
      })
    }
  }
}
</script>

<style>
  .layout-padding h5 {
    margin-top: 0px;
  }
</style>
