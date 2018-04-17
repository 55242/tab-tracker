<template>
  <v-layout>
    <v-flex xs6 offset-xs3>
      <div class="while elevation-2">
        <v-toolbar flat dense class="cyan" dark>
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar>
        <div class="pl-4 pr-4 pt-2 pb-2">
          <v-text-field
            name="email"
            label="Email"
            v-model="email"
            class="input-group--focused">
          </v-text-field>
          <br>
          <v-text-field
            name="password"
            label="Enter your password"
            hint="At least 8 characters"
            min="8"
            :append-icon="e3 ? 'visibility' : 'visibility_off'"
            :append-icon-cb="() => (e3 = !e3)"
            v-model="password"
            class="input-group--focused"
            :type="e3 ? 'password' : 'text'"
          ></v-text-field>
          <br>
          <div v-html="error" class="error"/>
          <br>
          <v-btn
            @click="register">
          Register
          </v-btn>
        </div>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null,
      e3: true
    }
  },
  methods: {
    async register () {
      try {
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  text-decoration-color: red;
}
</style>
