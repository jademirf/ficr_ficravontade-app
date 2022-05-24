<template>
  <q-page padding>
    <!-- content -->
    <q-card>
      <q-card-section>
        <div class="text-h4">Listagem de Usuários</div>
      </q-card-section>
      <q-card-section v-if="token">
        <q-list bordered separator>
          <q-item v-for="(user) in this.users" :key="user.id" clickable v-ripple>
            <q-item-section @click="() => $router.push(`/user/${user.id}`)">{{ user.name }}</q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
      <q-card-section v-else>
        <div class="text-body">Faça login para visualizar a lista de usuários</div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import jwtDecode from 'jwt-decode'
export default {
  name: 'UsersListPage',
  data () {
    return {
      token: undefined,
      users: []
    }
  },
  methods: {
    listUsers () {
      this.$api.defaults.headers.common.Authorization = 'Bearer ' + this.token
      this.$api.get('/users').then(response => {
        this.users = response.data
      })
    }
  },
  beforeMount () {
    if (window.sessionStorage.token) {
      this.token = window.sessionStorage.token
      console.log(jwtDecode(this.token))
      this.listUsers()
    }
  }
}
</script>
