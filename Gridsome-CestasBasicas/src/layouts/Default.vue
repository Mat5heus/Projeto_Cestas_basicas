<template>
  <v-app>
    <NavBar />
    <Snackbar :snack="snack" @onSnack="onSnackClick($event)"/>
    <v-main>
      <slot/> 
    </v-main>
    <Footer/>
  </v-app>
</template>

<script>
import NavBar from '~/components/NavBar.vue'
import Footer from '~/components/Footer.vue'
import ProgressCircular from '~/components/ProgressCircular.vue'
import Snackbar from '~/components/Snackbar.vue'

export default {
  components: {
    NavBar,
    Footer,
    ProgressCircular,
    Snackbar
  },
  data: () => ({
    snack: {
      multiLine: true,
      snackbar: true,
      text: `O botao foi clicado!`,
    } 
  }),
  methods: {
    onSnackClick(boo) {
      this.snack.snackbar = boo
    }
  }
}
</script>
