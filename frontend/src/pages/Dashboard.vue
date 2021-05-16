<template>
  <Layout>
    <v-container fluid >
      <v-row >
        <v-col cols="12" sm="3">
          <NavigationCard/>
        </v-col>
        <v-col>

          <!-- <v-container fluid> -->
            <v-row>
              <v-col 
                v-for="(edge, i) in $page.cesta.edges"
                :key="i"
                cols="12"
                sm="6"
              >

                <v-card
                  loading="progressive"
                  dark
                >
                  <div class="d-flex flex-no-wrap justify-space-between">
                    <div>
                    <v-card-title
                        class="text-h5"
                        v-text="edge.node.title"
                    ></v-card-title>

                    <v-card-subtitle
                        v-if="edge.node.description.length < 55"
                        v-text="edge.node.description"
                        class="mb-6"
                    >  
                    </v-card-subtitle>

                    <v-card-subtitle 
                        v-else
                        v-text="`${edge.node.description.substr(0, 53)}...`"
                    ></v-card-subtitle>

                    <v-card-actions>
                        <v-btn
                        class="ml-2 mt-5"
                        outlined
                        rounded
                        small
                        >
                        Doar Agora
                        </v-btn>
                    </v-card-actions>
                    </div>

                    <v-avatar
                    class="ma-3"
                    size="125"
                    tile
                    >
                    <v-img 
                        transition="fade-transition"
                        :src="`http://localhost:1337${edge.node.image.url}`"
                        :lazy-src="`http://localhost:1337${edge.node.image.formats.thumbnail.url}`"
                    >
                        <!-- <ProgressCircular/> -->
                    </v-img>
                    </v-avatar>
                  </div>
                </v-card>

              </v-col>
            </v-row>
          <!-- </v-container> -->
        
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>
<page-query>
query {
  cesta: allStrapiBasicBaskets (limit:10){
    edges{
      node {
        id
        title
        description
        price
        image {
          url
          formats {
            thumbnail {
              url
            }
          }
        }
      }
    }
  }
}
</page-query>

<script>
import NavigationCard from '~/components/NavigationDrawer.vue'
import ProgressCircular from '~/components/ProgressCircular.vue'
export default {
  metaInfo: {
    title: `Bem-Vindo!!`
  },
  components: {
    NavigationCard,
    ProgressCircular
  },
  data() {
    return {

    }
  }
  
}
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
