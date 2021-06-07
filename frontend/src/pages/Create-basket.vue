<template>
    <Layout>
        <v-container fluid>
            <v-row>
                <v-col cols="12" sm="3">
                    <NavigationCard/>
                </v-col>
                <v-col>
                    <v-forms>
                        <v-container>
                            <v-row>
                                <v-col class="text-center text-h4 font-weight-bold">
                                    Cadastrar cesta básica
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col >
                                    <v-text-field
                                        placeholder="Titulo"
                                        v-model="form.title"
                                        solo
                                        clearable
                                    ></v-text-field>
                                </v-col>
                                <v-col >
                                    <v-text-field
                                        v-model="form.price"
                                        placeholder="Custo"
                                        type="number"
                                        solo
                                        clearable
                                        :rules="[v => v >= 0 || 'Valor deve ser igual ou maior que 0']"
                                    ></v-text-field>
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col>
                                    <v-file-input
                                        label="Imagem de capa"
                                        solo
                                        prepend-icon="mdi-camera"
                                        @change="preview_image()"
                                        v-model="form.image"
                                    ></v-file-input>
                                </v-col>
                                <v-col>
                                    <v-select
                                        v-model="form.size"
                                        :items="sizes"
                                        label="Tamanho"
                                        solo
                                    ></v-select>
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col cols="6">
                                    <v-img
                                        max-height="150"
                                        max-width="250"
                                        :src="preview_url"
                                    ></v-img>
                                </v-col>
                                <v-col cols="6">
                                    <v-textarea
                                        v-model="form.description"
                                        solo
                                        label="Descrição"
                                    ></v-textarea>
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col>
                                    <v-btn 
                                       @click="save()" 
                                       dark
                                    >
                                        Cadastrar
                                    </v-btn>
                                </v-col>
                                <v-col>
                                    <v-btn
                                       to="/dashboard"
                                       dark
                                    >
                                        Cancelar
                                    </v-btn>
                                </v-col>
                            </v-row>
                        </v-container>
                    </v-forms>
                </v-col>
            </v-row>
        </v-container>
    </Layout>
</template>
<script>
import NavigationCard from '~/components/NavigationDrawer.vue'
import { GraphQLClient, gql } from 'graphql-request'

export default {
    components: {
        NavigationCard
    },
    data() {
        return {
            sizes: ['Pequena','Media','Grande'],
            preview_url: null,
            form: {
                title:'',
                price:null,
                description:'',
                size:'',
                image: null
            }
        }
    },
    methods: {
        preview_image() {
            console.log(this.form.image)
            this.preview_url = URL.createObjectURL(this.form.image)
        },
        async save() {
            const endpoint = 'http://localhost:1337/graphql'

            const graphQLClient = new GraphQLClient(endpoint)

            const mutation = gql`mutation {
                createBasicBasket ( input: {
                    data: {
                        title: "${this.form.title}",
                        description: "${this.form.description}",
                        price:${this.form.price},
                        sizes:${this.form.size}
                    }
                }) {
                    basicBasket {
                        title
                    }
                }
            }`
                            
            const data = await graphQLClient.request(mutation)

            if (data.basicBasket[0].title == this.title) {
                console.info("Sucesso!")
            }
            console.log(data)
        }

    }
}
</script>