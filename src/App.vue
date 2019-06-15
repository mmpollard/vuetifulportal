<template>
  <v-app>

    <v-toolbar app>
    <v-toolbar>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title>Title</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat>Link One</v-btn>
        <v-btn flat>Link Two</v-btn>
        <v-btn
          flat
          href="https://github.com/vuetifyjs/vuetify/releases/latest"
          target="_blank"
        >
          <span class="mr-2">Latest Release</span>
        </v-btn>
    </v-toolbar-items>
    </v-toolbar>
      <v-spacer></v-spacer>
      <router
      <v-btn
      v-if='authenticated' v-on:click='logout' id='logout-button'> Logout
      </v-btn>
      <v-btn
      v-else v-on:click='login' id='login-button'> Login
      </v-btn>
    </v-toolbar>

    <v-content>
      <HelloWorld/>
    </v-content>
          <router-view/>

  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'


export default {

    name: 'app',
  data: function () {
    return {
      authenticated: false
    }
  },
  created () {
    this.isAuthenticated()
  },
  watch: {
    // Everytime the route changes, check for auth status
    '$route': 'isAuthenticated'
  },
  methods: {
    async isAuthenticated () {
      this.authenticated = await this.$auth.isAuthenticated()
    },
    login () {
      this.$auth.loginRedirect('/')
    },
    async logout () {
      await this.$auth.logout()
      await this.isAuthenticated()

      // Navigate back to home
      this.$router.push({ path: '/' })
    }
  }
}
</script>
