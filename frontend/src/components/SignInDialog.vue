<template>
    <v-dialog
        transition="dialog-bottom-transition"
        max-width="600"
    >
        <template v-slot:activator="{ on, attrs }">
        <v-btn
            v-if="!user"
            v-model="user"
            dark
            v-bind="attrs"
            v-on="on"
        >
            Cadastrar
        </v-btn>
        </template>
        <template v-slot:default="dialog">
         <v-card 
            color="rgb(255, 198, 92)"
        >
            <v-toolbar
            dark
            >
                Nós faremos história juntos!
            </v-toolbar>
            <v-card-text>
            <div class="pa-12 pt-9 pb-5">
                 <v-container>
                    <v-row>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="firstName"
                                solo
                                label="Primeiro nome"
                                clearable
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                            <v-text-field
                                v-model="lastName"
                                solo
                                label="Segundo nome"
                                clearable
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-text-field
                                v-model="email"
                                solo
                                label="Email"
                                clearable
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-text-field
                                v-model="password"
                                solo
                                label="Senha"
                                clearable
                                :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                                :type="show1 ? 'text' : 'password'"
                                @click:append="show1 = !show1"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-container>
            </div>
            </v-card-text>
            <v-card-actions class="justify-end">
            <v-btn
                text
                @click="dialog.value = false"
            >
                Cancelar
            </v-btn>
            <v-btn
                text
                @click="addUser()"
            >
                Cadastrar
            </v-btn>
            </v-card-actions>
        </v-card>
        </template>
    </v-dialog>
</template>
<script>
import { GraphQLClient, gql } from 'graphql-request'

export default {
    data () {
        return {
        show1: false,
        firstName:'',
        lastName:'',
        email:'',
        user: $cookies.isKey("user"),
        password:'',
        dialog: {
            value: false
        },
        rules: {
            required: value => !!value || 'Required.',
            min: v => v.length >= 8 || 'Mínimo de 8 letras',
        },
        }
    }, mounted() {
        this.user = $cookies.isKey("user")
    },
    methods: {
        async addUser() {
            const endpoint = 'http://localhost:1337/graphql'

            const graphQLClient = new GraphQLClient(endpoint)
            const mutation = gql`
            
            mutation {
                createComumUser (input: {
                    data: {
                    Name:"${this.firstName} ${this.lastName}",
                    email: "${this.email}",
                    password: "${this.password}"
                    }
                }) {
                    comumUser {
                        id
                        Name
                        email
                    }
                }
                }
            `
            const data = await graphQLClient.request(mutation)
            if (data.comumUsers[0].email == this.email) {
                localStorage.id = btoa(data.comumUsers[0].id)
                window.location.href = '/dashboard'
            }
        },
    }
}
</script>