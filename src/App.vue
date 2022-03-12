<template>
  <nav>
    <p v-if="email">
      <small>Logged-in as {{ email }}</small>
    </p>
    <p v-else>
      <button @click="signIn" type="button" class="btn btn-primary">Google Log-in</button>
    </p>
    <router-link to="/">Home</router-link> |
    <router-link to="/dashboard">Dashboard</router-link>
  </nav>
  <router-view/>
</template>

<script>
import { inject } from 'vue'

export default {
  data() {
    return {
      email: null,
      authCode: null,
    }
  },
  methods: {
    async signIn() {
      this.email = await this?.$gAuth?.instance?.currentUser?.get()?.getBasicProfile()?.getEmail()
      if (this.email) {
        this.authCode = this.$gAuth.getAuthCode()
      } else {
        this?.$gAuth?.signIn()
      }
    },
    async signOut() {
      await this.$gAuth.signOut()
      await this.$gAuth.signIn()
    },
    authenticated() {
      return this.authCode != null
    }
  },
  setup() {
    const Vue3GoogleOauth = inject("Vue3GoogleOauth")
    return {
      Vue3GoogleOauth,
    };
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
