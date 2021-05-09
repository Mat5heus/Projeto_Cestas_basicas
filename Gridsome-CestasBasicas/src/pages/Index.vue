<template>
    <Layout>
        <v-parallax
         height="700"
         :src="`http://localhost:1337${$static.index.background.url}`"
         :srcset="`http://localhost:1337${$static.index.background.formats.medium.url}`"
         :alt="$static.index.background.caption"
        >
            <div class="text-h2 font-weight-bold text-center">{{ $static.index.title }}</div>
        </v-parallax>
        <v-container>
            <v-row>
                <v-col cols="12" sm="12">
                    <h2 class="text-h3 font-weight-medium text-center">Participe da nossa comunidade</h2>
                    
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12">
                    <p class="text-center">{{ $static.index.description }}</p>
                </v-col>
            </v-row>
        </v-container>
    </Layout>
</template>
<static-query>
query {
  index: strapiIndex(id:1) {
    id
    title
    description
    background {
      caption
      formats {
        medium {
          url
        }
      }
      url
    }
  }
}
</static-query>