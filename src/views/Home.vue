<template>
  <v-container fluid class="align-center">
    <section>
      <h1>Acetumour</h1>

      <img alt='home' src='../assets/homeBg.svg'>
    </section>
    <div class="footer">Copyright &copy; 2020 Invisble vision</div>
  </v-container>
</template>

<script>

export default {
  name: 'Home',
  mounted () {
  },
  components: {
  }
}
</script>

<style scoped>
  h1 {
    font-size: 8vw;
  }

  section {
    padding: 30px 70px;
    padding-bottom: 0px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 83vh;
  }
  img {
    width: 700px;
    max-width: 90%;
    padding-top: 50px;
  }

  div.footer {
    font-size: 0.8rem;
    color: #999;
    text-align: center;
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
