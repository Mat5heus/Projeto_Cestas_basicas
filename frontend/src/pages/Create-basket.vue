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
                                        solo
                                        clearable
                                    ></v-text-field>
                                </v-col>
                                <v-col >
                                    <v-text-field
                                        placeholder="Custo"
                                        solo
                                        clearable
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
                                        v-model="image"
                                    ></v-file-input>
                                </v-col>
                                <v-col>
                                    <v-select
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
                                        :src="url"
                                    ></v-img>
                                </v-col>
                                <v-col cols="6">
                                    <v-textarea
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
export default {
    components: {
        NavigationCard
    },
    data() {
        return {
            sizes: ['Pequena','Média','Grande'],
            image: null,
            url: null
        }
    },
    methods: {
        preview_image() {
            this.url = URL.createObjectURL(this.image)
        }

    }
}
</script>