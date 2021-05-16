<template>
  <v-app>
    <NavBar :snack="snack" @onSnack="onSnackClick($event)"/>
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
      snackbar: false,
      text: ``,
    } 
  }),
  methods: {
    onSnackClick(boo) {
      this.snack.snackbar = boo
    }
  }
}
</script>
