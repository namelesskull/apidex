<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card>
              <v-card-title class="headline"> Login </v-card-title>
              <v-card-text>
                <v-form @submit.prevent="login">
                  <v-text-field
                    v-model="username"
                    label="Username"
                    required
                  ></v-text-field>
                  <v-text-field
                    v-model="password"
                    label="Password"
                    type="password"
                    required
                  ></v-text-field>
                  <v-btn color="primary" @click="login">Login</v-btn>
                </v-form>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
    }
  },
  methods: {
    login() {
      // Di sini Anda dapat menambahkan logika login Anda.
      // Anda dapat mengirimkan permintaan ke server atau melakukan verifikasi lokal.
      // Contoh:
      if (this.username === 'user' && this.password === 'password') {
        this.$router.push('/dashboard') // Ganti rute dengan rute dashboard Anda.
      } else {
        alert('Login gagal. Coba lagi.')
      }
    },
  },
}
</script>
