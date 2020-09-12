<template>
  <q-table
    :title="`Orçamento de ${senderCompany} para ${receiverCompany}`"
    :columns="tableColumns"
    :data="tableData"
    row-key="name"
  >
    <template v-slot:top-right>
      <q-btn
        color="primary"
        icon-right="archive"
        label="Export to csv"
        no-caps
        @click="exportTable"
      />
    </template>
    <template v-slot:body="props">
      <q-tr :props="props">
        <q-td key="desc" :props="props">
          {{ props.row.name }}
          <q-popup-edit v-model="props.row.name" buttons>
            <q-input v-model="props.row.name" dense autofocus counter />
          </q-popup-edit>
        </q-td>
        <q-td key="quantity" :props="props">
          {{ props.row.storageQuantity }}
          <q-popup-edit v-model="props.row.storageQuantity" buttons>
            <q-input v-model="props.row.storageQuantity" dense autofocus />
          </q-popup-edit>
        </q-td>

        <q-td key="price" :props="props">
          R$ {{ props.row.price }}
          <q-popup-edit v-model="props.row.price" buttons>
            <q-input v-model="props.row.price" dense autofocus />
          </q-popup-edit>
        </q-td>
      </q-tr>
    </template>
  </q-table>
</template>

<script>
import { exportFile } from 'quasar'

function wrapCsvValue (val, formatFn) {
  let formatted = formatFn !== undefined ? formatFn(val) : val

  formatted =
    formatted === undefined || formatted === null ? '' : String(formatted)

  formatted = formatted.split('"').join('""')
  /**
   * Excel accepts \n and \r in strings, but some other CSV parsers do not
   * Uncomment the next two lines to escape new lines
   */
  // .split('\n').join('\\n')
  // .split('\r').join('\\r')

  return `"${formatted}"`
}
export default {
  props: {
    senderCompany: {
      type: String,
      required: true
    },
    receiverCompany: {
      type: String,
      required: true
    },
    products: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      tableColumns: [
        {
          name: 'desc',
          label: 'Produto',
          field: row => row.name,
          align: 'left'
        },
        {
          name: 'quantity',
          label: 'Quantidade em Estoque',
          field: 'storageQuantity',
          align: 'left'
        },
        {
          name: 'price',
          label: 'Preço',
          field: 'price',
          align: 'left'
        }
      ],
      tableData: [{ name: 'Leite', storageQuantity: '10', price: '20.0' }]
    }
  },
  mounted () {
    this.tableData = Array.from(this.products)
  },
  methods: {
    exportTable () {
      // naive encoding to csv format
      // Change this generate it on the API
      const content = [this.tableColumns.map(col => wrapCsvValue(col.label))]
        .concat(
          this.tableData.map(row =>
            this.tableColumns
              .map(col =>
                wrapCsvValue(
                  typeof col.field === 'function'
                    ? col.field(row)
                    : row[col.field === undefined ? col.name : col.field],
                  col.format
                )
              )
              .join(',')
          )
        )
        .join('\r\n')

      const status = exportFile('table-export.csv', content, 'text/csv')

      if (status !== true) {
        this.$q.notify({
          message: 'Browser denied file download...',
          color: 'negative',
          icon: 'warning'
        })
      }
    }
  }
}
</script>

<style></style>
