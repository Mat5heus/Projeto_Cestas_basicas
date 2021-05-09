<template>
  <v-card
    height="390"
    width="300"
    outlined
  >
    <v-navigation-drawer
      permanent
      floating
      width="100%"
      left
    >
      <v-row
        class="fill-height"
        no-gutters
      >
        <v-navigation-drawer
          color="rgb(255, 198, 92)"
          mini-variant
          mini-variant-width="56"
          permanent
        >
          <v-list-item 
            class="px-2"
            to="/profile"
          >
            <v-list-item-avatar>
              <v-avatar>
                
                <v-img 
                  v-if="image.src != null"
                  :src="image.src">
                </v-img> 
                <v-icon
                  v-else
                 dark>
                  mdi-account-circle
                </v-icon>
              </v-avatar>
            </v-list-item-avatar>
          </v-list-item>

          <v-divider></v-divider>
          <v-list
            dense
            nav
          >
            <v-list-item
              v-for="item in items"
              :key="item.title"
              :to="item.link"
            >
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-navigation-drawer>

        <v-list class="grow">
          <v-list-item
            v-for="{title, link } in navOptions"
            :key="title"
            title
            :to="link"
          >
            <v-list-item-title v-text="title"></v-list-item-title>
          </v-list-item>
        </v-list>
      </v-row>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
import { GraphQLClient, gql } from 'graphql-request'
export default {
  async mounted() {
    const endpoint = 'http://localhost:1337/graphql'

    let id = atob(localStorage.id)

    const graphQLClient = new GraphQLClient(endpoint)
    const query = gql`{
      comumUser(id:${id}) {
        Name
        image {
          url
        }
      }
    }
    `
    await graphQLClient.request(query).then(data => {
      if(data.comumUser.image.url != null) {
        this.image.src = `http://localhost:1337${data.comumUser.image.url}`
      }
    })
  },
  data() {
    return {
      image: {
        src:''
      },
      items: [
        { title: 'Home', icon: 'mdi-view-dashboard', link:'/' },
        { title: 'About', icon: 'mdi-forum', link:'/about' },
      ],
      navOptions: [
        { title:'Inicio', link: '/dashboard'},
        { title:'Amigos', link:'/friends'},
        { title:'Meus Produtos', link:'/add-product'},
        { title:'Criar Cesta', link:'/create-basket'},
        { title:'Perfil', link:'/profile'},
      ],
      mini: true,
    }
  }
}
</script>