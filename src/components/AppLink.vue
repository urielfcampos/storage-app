<template>
  <q-item
    clickable
    tag="a"
    target="_blank"
    @click="navigate"
  >
    <q-item-section
      v-if="icon"
      avatar
    >
      <q-icon :name="icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
      <q-item-label caption>
        {{ caption }}
      </q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
export default {
  name: 'AppLink',
  props: {
    title: {
      type: String,
      required: true
    },

    caption: {
      type: String,
      default: ''
    },

    path: {
      type: String,
      default: '/'
    },

    icon: {
      type: String,
      default: ''
    }
  },
  methods: {
    navigate () {
      this.$router.push(this.path)
    }
  }
}
</script>
