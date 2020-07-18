<template>
  <v-container fluid>
    <v-overlay :value="loading" absolute>
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
    <section>
      <div style="text-align: center; width: 50%">
        <img :src="thirdParty.info.avatar_url" alt="avatar"/>
        <h3>{{ thirdParty.info.login }}</h3>
      </div>
      <div style="width: 50%">
        <v-form style="width: 450px">
          <v-container>
            <v-text-field
              v-model="backend.email"
              label="Email address"
              outlined
              :disabled="!edit"
            ></v-text-field>
            <v-text-field
              v-model="backend.phone"
              label="Phone number"
              outlined
              :disabled="!edit"
            ></v-text-field>
            <v-btn outlined medium @click="Edit" style="width: 100px; margin-right: 20px">Edit</v-btn>
            <v-btn outlined medium @click="Submit" style="width: 100px;">Submit</v-btn>
          </v-container>
        </v-form>
      </div>
    </section>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Profile',
  data () {
    return {
      loading: true,
      thirdParty: JSON.parse(window.localStorage.getItem('user')),
      backend: {},
      edit: false
    }
  },
  async mounted () {
    await axios
      .get(`/api/user/info?user=${this.thirdParty.info.id}`)
      .then(resp => {
        console.log(resp.data)
        this.backend = resp.data
        this.loading = false
      })
    console.log(this.thirdParty.info)
  },
  components: {
  },
  methods: {
    Edit: function () {
      this.edit = true
    },
    Submit: function () {
      if (!this.edit) return
      this.edit = false
      axios
        .post(`/api/user/info?user=${this.thirdParty.info.id}`, this.backend)
        .then(resp => {
          if (resp.data) {

          }
        })
        .catch(err => {
          console.log(err)
        })
    }
  }
}
</script>

<style scoped>
  h1 {
    font-size: 8vw;
  }

  section {
    padding: 30px 70px;
    display: flex;
    justify-content: space-around;
    align-items: center;
  }

  img {
    width: 300px;
    max-width: 80%;
  }

  @media (max-width: 700px) {

    section {
      flex-direction: column;
      padding: 20px 8px;
    }

    section.reverse {
      flex-direction: column-reverse;
    }
  }
</style>
