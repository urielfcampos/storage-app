<template>
  <q-page class="row justify-center q-pt-xl">
    <section class="column size">
      <div class="row justify-around">
        <q-select
          outlined
          v-model="selectedSender"
          :options="companies"
          label="Remetente"
          class="q-pb-md col-5"
        />
        <q-select
          outlined
          v-model="selectedReceiver"
          :options="companies"
          label="Destinatario"
          class="q-pb-md col-5"
        />
      </div>
      <div class="col-4">
        <product-table :company="selectedSender"> </product-table>
      </div>
      <div>
           <q-btn label="Adicionar produto"></q-btn>
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
      selectedSender: '',
      selectedReceiver: '',
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
