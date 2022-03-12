<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/dashboard">Dashboard</router-link>
    <p v-if="email">
      <small>Logged-in as {{ email }}. </small>
      <a href="#" @click="signOut">
        <small>Sign-out</small>
      </a>
    </p>
    <p v-else>
      <button @click="signIn" type="button" class="btn btn-primary mt-5">Google Log-in</button>
    </p>
    <p v-show="loginError" class="text-danger">
      <small>Try again</small>
    </p>
  </nav>
  <router-view/>
</template>

<script>
import { inject } from 'vue'

export default {
  data() {
    return {
      email: null,
      loginError: false,
    }
  },
  methods: {
    async signIn() {
      this.loginError = false

      const result = await this?.$gAuth?.signIn()?.catch(() => {
        return null
      })

      if (result) {
        this.email = result.getBasicProfile().getEmail()
        if (!this.email) {
          this.loginError = true
        }
      } else {
        this.loginError = true
      }
    },
    async signOut() {
      await this.$gAuth.signOut()
      this.email = null
    },
    authenticated() {
      return this.email != null
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
