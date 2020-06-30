<template>
  <div class="about">
    <h1>{{ tip }}</h1>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Profile',
  data () {
    return {
      tip: 'loginning with github'
    }
  },
  mounted () {
    const code = this.$route.query.code
    console.log(code)
    if (!code || this.$store.user === '') {
      window.location.href = '/'
      return
    }
    axios
      .post('/api/user', { code: code, platform: 'GITHUB' })
      .then(resp => {
        if (resp.data) {
          this.tip = 'This is a profile page'
        }
      })
      .catch(function (err) {
        console.log(err)
        window.location.href = '/'
      })
  },
  components: {
  }
}
</script>
