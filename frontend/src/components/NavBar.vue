<template>
  <div>
    <v-app-bar
      color="rgb(255, 165, 2)"
      dense
      dark
    >

      <v-toolbar-title>{{ title }}</v-toolbar-title>

      <v-btn
        v-for="{link, title} in footerLinks"
        :key="link"
        color="white"
        text
        class=""
        :to="link"
      >
        {{ title }}
      </v-btn>

      <v-spacer></v-spacer>
      
      <LoginDialog :snack="snack" @onSnack="onSnackClick($event)"/>
      <SignInDialog/>
      <LogoutBtn/>
      <v-menu
        left
        bottom
      >
        <v-list>
          <v-list-item
            v-for="n in 5"
            :key="n"
            @click="() => {}"
          >
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </div>
</template>
<script>
import LoginDialog from '~/components/LoginDialog.vue'
import SignInDialog from '~/components/SignInDialog.vue'
import LogoutBtn from '~/components/LogoutBtn.vue'

export default {
  components : {
     LoginDialog,
     SignInDialog,
     LogoutBtn
  },
  props: ['snack'],
  data() { 
    return { 
      title:"Associação de Assistencia",
      expand: false,
      footerLinks: [
        { title:'Início', link:'/' },
        { title:'Sobre nós', link:'/about' },
        { title:'Equipe', link:'/team'},
        { title:'Serviços', link:'/services'},
        { title:'Contato', link:'/contact'}
      ]
    }
  },
  methods: {
    onSnackClick(event) {
      
    }
  }
}
</script>
