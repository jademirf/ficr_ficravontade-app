<template>
  <q-page padding>
    <q-card>
      <q-card-section>
        <div class="text-h4">Signin</div>
      </q-card-section>
      <q-card-section>
        <q-input type="text" v-model="user.login" label="Login" name="login" />
        <q-input type="text" v-model="user.pass" label="pass" name="pass" />
      </q-card-section>
    <q-card-section>
      <q-btn @click="logar">Login</q-btn>
    </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'UserSignin',
  data () {
    return {
      user: {
        login: 'desmeninho@gmail.com',
        pass: 'senhaSuperSecreta1234'
      }
    }
  },
  methods: {
    logar () {
      this.$api.post('/signin', { user: this.user }).then(response => {
        console.log(response.data)
        window.sessionStorage.token = response.data.token
      }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>
