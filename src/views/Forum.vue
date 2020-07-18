<template>
  <v-container fluid class="d-flex flex-column align-center justify-center">
    <v-overlay :value="loading" absolute>
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
    <v-row align="center">
      <v-col class="d-flex" cols="12" sm="6">
        <v-overflow-btn
          class="my-2"
          :items="threads"
          label="choose threads"
          editable
          target="#all"
          :val="thread"
          append-icon-cb="choose(text)"
        ></v-overflow-btn>
      </v-col>
      <v-col class="d-flex" cols="12" sm="6">
        <v-text-field
          style="width: 600px"
          prepend-inner-icon="mdi-magnify"
          placeholder="search for post"
          rounded
          outlined
        />
      </v-col>
    </v-row>
    <v-list two-line subheader style="width: 80%">
      <v-subheader>POSTS</v-subheader>
      <v-list-item
        v-for="item in items"
        :key="item.title"
      >
      <v-list-item-content>
        <v-list-item-title v-text="item.title" />
        <v-list-item-subtitle v-text="subtitle(item.time, item.author)" />
        {{ content(item.content) }}
      </v-list-item-content>

      <v-list-item-action>
        <v-btn icon>
          <v-icon color="grey lighten-1">mdi-information</v-icon>
        </v-btn>
      </v-list-item-action>
      </v-list-item>
    </v-list>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Forum',
  data () {
    return {
      loading: true,
      threads: [],
      thread: 'uuu',
      items: [
        { author: 'Tim', time: 'Jan 9, 2014', title: 'Photos', content: 'Data initialization for global variables happens in the initial system state. All process local variables are initialized at process instantiation. The moment of creation and initialization of a local variable is independent of the precise place within the proctype body where the variable declaration is placed.' },
        { author: 'Denial', time: 'Jan 17, 2014', title: 'Recipes', content: 'Data initialization for global variables happens in the initial system state. All process local variables are initialized at process instantiation. The moment of creation and initialization of a local variable is independent of the precise place within the proctype body where the variable declaration is placed.' },
        { author: 'Qertyrut', time: 'Jan 28, 2014', title: 'Work', content: 'Data initialization for global variables happens in the initial system state. All process local variables are initialized at process instantiation. The moment of creation and initialization of a local variable is independent of the precise place within the proctype body where the variable declaration is placed.' }
      ]
    }
  },
  components: {
  },
  async mounted () {
    const code = this.$route.query.code
    console.log('mounted')
    if (!code && !window.localStorage.getItem('user')) {
      this.loading = false
      window.location.href = '/'
      return
    }
    if (code) {
      await axios
        .post('/api/user', { code: code, platform: 'GITHUB' })
        .then(resp => {
          if (resp.data) {
            window.localStorage.setItem('user', JSON.stringify(resp.data))
            window.location.href = '/forum'
          }
        })
        .catch(function (err) {
          console.log(err)
          window.location.href = '/'
        })
    }
    await axios
      .get('api/forum/t/all')
      .then(resp => {
        if (resp.data) {
          console.log(resp.data)
          this.loading = false
          this.threads = resp.data
        }
      })
      .catch(err => {
        console.log(err)
      })
  },
  methods: {
    subtitle (time, author) {
      return `Posted by ${author}, ${time}`
    },
    content (text) {
      if (text.length > 200) {
        return text.substring(0, 200) + '...'
      } else {
        return text
      }
    },
    choose (thread) {
      console.log(thread)
    }
  }
}
</script>

<style scoped>

</style>
