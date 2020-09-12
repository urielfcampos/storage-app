<template>
  <q-page class="row justify-center q-pt-xl">
    <section class="column size q-gutter-lg">
      <div class="row justify-between">
        <q-select
          outlined
          v-model="selectedSender"
          :options="companies"
          label="Remetente"
          class="q-pb-md col-5"
          :error="isValid"
        />
        <q-select
          outlined
          v-model="selectedReceiver"
          :options="companies"
          label="Destinatario"
          class="q-pb-md col-5"
          :error="isValid"
        />
      </div>
      <div class="col-sm-4 col-md-3">
        <order-table :senderCompany="selectedSender" :receiverCompany="selectedReceiver"> </order-table>
      </div>
      <div class="row justify-between">
        <q-btn class="col-3" label="Adicionar produto" color="info"></q-btn>
        <q-btn class="col-3" label="Criar orçamento" color="positive"></q-btn>
      </div>
    </section>
  </q-page>
</template>

<script>
import orderTable from 'components/orders/orderTable'
export default {
  components: { 'order-table': orderTable },
  data () {
    return {
      selectedSender: '',
      selectedReceiver: '',
      companies: ['Brazil Merchant', 'Brasil Comercio', 'U F Campos']
    }
  },
  computed: {
    isValid: function () {
      if (this.selectedSender || this.selectedReceiver) {
        return this.selectedSender === this.selectedReceiver
      }
      return false
    }
  }

}
</script>

<style scoped>
.size {
  width: 70%;
}
</style>
