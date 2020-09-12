<template>
  <q-page class="row justify-center q-pt-xl">
    <section class="column size">
      <div class="row">
        <q-select
          outlined
          v-model="selectedCompany"
          :options="companies"
          label="Escolher Empresa"
          class="q-pb-md col-3"
        />
      </div>
      <div>
        <product-table :company="selectedCompany" :tableData="tableData"> </product-table>
      </div>
      <div class="row q-mt-lg q-gutter-sm justify-between">
        <q-input v-model="product.name" class="col-3" label="Nome"></q-input>
        <q-input v-model="product.price" class="col-3" label="Preço"></q-input>
        <q-input v-model="product.storageQuantity" class="col-3" label="Quantidade"></q-input>
        <div class="q-mt-lg">
          <q-btn round color="primary" icon="add" @click="addProduct"></q-btn>
        </div>
      </div>
      <div>

      </div>
    </section>
  </q-page>
</template>

<script>
import ProductTable from 'components/storage/productTable'
export default {
  components: { 'product-table': ProductTable },
  data () {
    return {
      selectedCompany: 'Brazil Merchant',
      companies: ['Brazil Merchant', 'Brasil Comercio', 'U F Campos'],
      tableData: [],
      product: {
        name: '',
        price: '',
        storageQuantity: ''
      },
      formIsvalid: true
    }
  },
  methods: {
    addProduct () {
      const isValid = this.validateForm()
      if (isValid) {
        this.tableData.push(Object.assign({}, this.product))
        this.clearForm()
      }
      this.showNotification(isValid)
    },
    clearForm () {
      for (const form in this.product) {
        this.product[form] = ''
      }
    },
    showNotification (result) {
      if (result) {
        this.$q.notify({ message: 'Produto adicionado', color: 'positive', position: 'top' })
      } else {
        this.$q.notify({ message: 'Ocorreu um erro', color: 'negative', position: 'top' })
      }
    },
    validateForm () {
      for (const value in this.product) {
        if (this.product[value].length === 0) {
          return false
        } else {
          return true
        }
      }
    }
  }
}
</script>

<style scoped>
.size {
  width: 70%;
}
</style>
