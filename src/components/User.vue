<template>
  <v-sheet style="padding: 30px 10px 20px 0px;">
    <h2 style="margin-left: 20px;">开发中...</h2>
    <v-divider></v-divider>
    <!-- Function List -->
    <v-list shaped>
      <v-list-item v-if="!user">
        <v-list-item-icon>
          <v-icon>mdi-account-circle</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>xx登陆</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item v-if="user">
        <v-list-item-icon>
          <v-icon>mdi-logout</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>登出</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-sheet>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'User',
  computed: {
    ...mapState(['user'])
  }
}
</script>
