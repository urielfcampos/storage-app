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
        <product-table :company="selectedCompany"> </product-table>
      </div>
    </section>
  </q-page>
</template>

<script>
import ProductTable from 'components/productTable'
export default {
  components: { 'product-table': ProductTable },
  data () {
    return {
      selectedCompany: 'Brazil Merchant',
      companies: ['Brazil Merchant', 'Brasil Comercio', 'U F Campos']
    }
  }
}
</script>

<style scoped>
.size {
  width: 70%;
}
</style>
