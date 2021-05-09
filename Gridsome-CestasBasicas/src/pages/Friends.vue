<template>
    <Layout>
        <v-container class="mt-3" fluid>
            <v-row>
                <v-col cols="12" sm="3">
                  <NavigationCard/>
                </v-col>
                <v-col>
                  <v-container>
                    <v-row>
                      <v-col cols="12" class="text-center text-h4">
                    Pessoas que você talvez conheça
                      </v-col>
                      <v-col cols="12" sm="4" :key="edge.node.id" 
                    v-for="(edge) in $page.allStrapiComumUsers.edges.filter( edge => edge.node.id != user.id )">
                    
                        <template >
                          <v-card
                            class="mx-auto"
                            max-width="344"
                            outlined
                          >
                            <v-list-item three-line>
                              <v-list-item-content>
                                <div class="overline mb-4">
                                  Recomendado
                                </div>
                                <v-list-item-title class="headline mb-1">
                                  {{ edge.node.Name }}
                                </v-list-item-title>
                                <v-list-item-subtitle
                                  v-if="edge.node.bio == ''"
                                  class="pb-4"
                                >
                                {{ edge.node.bio }}
                                </v-list-item-subtitle>
                                <v-list-item-subtitle
                                  v-else
                                  class="pb-4"
                                >
                                {{ edge.node.bio }}
                                </v-list-item-subtitle>

                              </v-list-item-content>

                              <v-list-item-avatar
                                tile
                                size="80"
                                color="grey"
                              >
                                <v-avatar
                                  color="primary"
                                  size="128"
                                  
                                >
                                  <v-img
                                      v-if="edge.node.image != null"
                                      id="userPicture"
                                      :src="`http://localhost:1337${edge.node.image.url}`"
                                      alt=""
                                  ></v-img>
                                  <v-icon 
                                      v-else
                                      dark
                                  >
                                  mdi-account-circle
                                  </v-icon>
                                </v-avatar>
                              </v-list-item-avatar>
                            </v-list-item>

                            <v-card-actions>
                              <v-btn
                                outlined
                                rounded
                                text
                              >
                                Seguir
                              </v-btn>
                            </v-card-actions>
                          </v-card>
                        </template>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-col>
                
            </v-row>
        </v-container>
    </Layout>
</template>
<page-query>
query {
  allStrapiComumUsers {
    edges {
      node {
        id
        Name
        bio
        image {
          url
        }
        friend_users {
          id
        }
      }
    }
    totalCount
    pageInfo {
      currentPage
      totalPages
      hasNextPage
      hasPreviousPage
    }
  }
}
</page-query>
<script>
import NavigationCard from '~/components/NavigationDrawer.vue'
export default {
   components: {
    NavigationCard
  },
  data() {
    return {
      user: {
        id: atob($cookies.get('user'))
      }
    }
  }
}
</script>