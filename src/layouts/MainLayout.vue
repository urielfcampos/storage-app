<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          Controle de Estoque
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>
        <AppLink
          v-for="link in links"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import AppLink from 'components/AppLink.vue'

const links = [
  {
    title: 'Estoque',
    caption: 'Verificar estoque',
    icon: 'school',
    path: 'storage'
  },
  {
    title: 'Orçamentos',
    caption: 'Criação de orçamentos',
    icon: 'code',
    path: 'orders'
  }
]

export default {
  name: 'MainLayout',
  components: { AppLink },
  data () {
    return {
      leftDrawerOpen: false,
      links: links
    }
  }
}
</script>
