<template>
  <v-app>
    <v-app>
    <Bar @open="userMenu = true" />
    <v-main>
      <transition name="fade" mode="out-in">
        <router-view />
      </transition>
    </v-main>
    <v-navigation-drawer
      app
      right
      temporary
      width="300px"
      v-model="userMenu"
    >
      <user />
    </v-navigation-drawer>
  </v-app>
  </v-app>
</template>

<script>
import Bar from '@/components/Bar.vue'
import User from '@/components/User.vue'
export default {
  name: 'App',

  components: {
    Bar, User
  },
  data () {
    return {
      userMenu: false
    }
  }
}
</script>
