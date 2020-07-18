<template>
  <v-sheet style="padding: 30px 10px 20px 0px;">
    <h2 style="margin-left: 20px;">Sign in</h2>
    <v-divider></v-divider>
    <!-- Function List -->
    <v-list shaped>
      <v-list-item v-if="!user" @click="Githublogin">
        <v-list-item-icon>
          <img alt="Github" src="../assets/github.png" style="max-width: 30px;" />
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Login with Github</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item v-if="user" @click="Jump('/profile')">
        <v-list-item-icon>
          <v-icon>mdi-account</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Profile</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item v-if="user" @click="Jump('/forum')">
        <v-list-item-icon>
          <v-icon>mdi-forum</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Forum</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item v-if="user" @click="Logout">
        <v-list-item-icon>
          <v-icon>mdi-logout</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Logout</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-sheet>
</template>

<script>

const config = {
  oauth_uri: 'https://github.com/login/oauth/authorize',
  redirect_uri: 'http://localhost:8080/forum',
  client_id: '368c3543fd57241028ca',
  client_secret: 'a5fbe2fb9e69bf21b24cf533edef8c65da3ac3cd'
}

export default {
  name: 'User',
  data () {
    return {
      user: window.localStorage.user
    }
  },
  methods: {
    Githublogin () {
      window.location.href = `${config.oauth_uri}?client_id=${config.client_id}&redirect_uri=${config.redirect_uri}`
    },
    Logout () {
      this.Jump('/')
      window.localStorage.clear()
    },
    Jump (url) {
      window.location.href = url
    }
  }
}
</script>
