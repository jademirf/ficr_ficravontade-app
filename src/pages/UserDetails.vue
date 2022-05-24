<template>
  <q-page padding>
    <q-card>
      <q-card-section>
        <div class="text-h4">{{ user?.name }}</div>
      </q-card-section>
      <q-card-section>
        <div class="text-h5">{{ user?.email }}</div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'UserDetails',
  data () {
    return {
      user: {
        name: '',
        email: ''
      }
    }
  },
  beforeMount () {
    this.$api.defaults.headers.common.Authorization = 'Bearer ' + window.sessionStorage.token
    const url = 'users/' + this.$route.params.id
    this.$api.get(url).then(response => {
      this.user = response.data.user
    })
  }
}
</script>
