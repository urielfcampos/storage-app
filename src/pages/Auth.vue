<template>
  <q-page class="flex flex-center">
    <q-card class="login-card flex flex-center">
      <q-card-section>
        <img alt="Quasar logo" src="~assets/quasar-logo-full.svg" />
      </q-card-section>
      <q-card-section class="full-width">
        <q-input
          v-model="username"
          label="Usuário"
          :rules="[val => (val && val.length > 0) || 'Please type something']"
        ></q-input>
        <q-input
          v-model="password"
          label="senha"
          :type="isPwd ? 'password' : 'text'"
          :rules="[val => (val && val.length > 0) || 'Please type something']"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>
      </q-card-section>
      <q-card-actions class="full-width">
        <q-btn
          color="primary"
          size="lg"
          class="full-width"
          label="Entrar"
        ></q-btn>
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      username: '',
      password: '',
      isPwd: true
    }
  }
}
</script>

<style scoped>
.login-card {
  width: 25%;
  height: 25%;
}
</style>
