<template>
    <Layout>
        <v-container fluid >
            <v-row >
                <v-col cols="12" sm="3">
                    <NavigationCard/>
                </v-col>
                <v-col>
                    <v-container fluid>
                    <v-row>
                        <v-col 
                            v-for="(edge, i) in $page.products.edges"
                            :key="i"
                            cols="12"
                            sm="6"
                        >
                            <v-card
                                dark
                            >
                            <div class="d-flex flex-no-wrap justify-space-between">
                                <div>
                                <v-card-title
                                    class="text-h5"
                                    v-text="edge.node.title"
                                ></v-card-title>

                                <v-card-subtitle
                                    v-if="edge.node.description.length < 34"
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
                                    Saiba mais
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
                                >
                    
                                </v-img>
                                </v-avatar>
                            </div>
                            </v-card>

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
  products: allStrapiProducts {
    edges {
      node {
        id
        title
        description
        Price
        image {
          url
        }
      }
    }
  }
}
</page-query>
<script>
import NavigationCard from '~/components/NavigationDrawer.vue'
export default {
    components: {
      NavigationCard  
    }
}
</script>