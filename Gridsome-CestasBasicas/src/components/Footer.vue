<template>
  <v-footer
    color="rgb(255, 184, 51)"
    padless
  >
    <v-row
      justify="center"
      no-gutters
    >
      <v-btn
        v-for="{link, title} in footerLinks"
        :key="link"
        color="white"
        text
        rounded
        class="my-2"
        :to="link"
      >
        {{ title }}
      </v-btn>
      <v-col
        class="py-4 text-center white--text"
        cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>
<script>
export default {
    data() {
        return {
            footerLinks: [
              { title:'Início', link:'/' },
              { title:'Sobre nós', link:'/about' },
              { title:'Equipe', link:'/team'},
              { title:'Serviços', link:'/services'},
              { title:'Contato', link:'/contact'}
            ]
        }
    }
    
}
</script>
