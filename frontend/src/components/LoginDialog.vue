<template>
   
    <v-dialog
        transition="dialog-bottom-transition"
        max-width="600"
    >
        <template
         v-slot:activator="{ on, attrs }"
         
        >
        <v-btn
            v-if="!user"
            dark
            v-bind="attrs"
            v-on="on"
            class="mr-2 ml-1"
        >
            Entrar
        </v-btn>
        </template>
        <template v-slot:default="dialog">
        <v-card 
            color="rgb(255, 198, 92)"
        >
            <v-toolbar
            dark
            >
                Bem-vindo de volta!
            </v-toolbar>
            <v-card-text>
            <div class="pa-12 pb-7">
                <v-container>
                    <v-row>
                        <v-col>
                            <v-text-field
                                v-model="email"
                                :rules="emailRules"
                                solo
                                label="Email"
                                clearable
                                v-on:keyup.enter="logar()"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-text-field
                                v-model="password"
                                solo
                                :rules="passwordRules"
                                label="Senha"
                                clearable
                                :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                                :type="show1 ? 'text' : 'password'"
                                @click:append="show1 = !show1"
                                v-on:keyup.enter="logar()"
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
                @click="logar()"
            >
                Entrar
            </v-btn>
            </v-card-actions>
        </v-card>
        </template>
    </v-dialog>
</template>
<script>
import { GraphQLClient, gql } from 'graphql-request'

export default {
    props: ['snack'],
    data () {
        return {
            show1: false,
            email: ''.toLowerCase(),
            password: '',
            user: $cookies.isKey("user"),
            multiLine: true,
            snackbar: false,
            text: `Email e/ou senha incorreto.`,
            dialog: {
                value: false
            },
            passwordRules: [
                value => !!value || 'Obrigatório.',
                v => v.length >= 8 || 'Mínimo de 8 letras'
            ],
            emailRules: [
                value => !!value || 'Obrigatório.',
                v => /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/.test(v)
                || "Email invalido!"
            ]
        }
    },
    methods: {
        async logar() {
            const endpoint = 'http://localhost:1337/graphql'

            const graphQLClient = new GraphQLClient(endpoint)
            const mutation = gql`
            query {
                comumUsers(where: {email: "${this.email}", password: "${this.password}"}) {
                    id
                    email
                }
            }
            `
            const data = await graphQLClient.request(mutation)
            
            if (typeof data.comumUsers[0] !== "undefined") {
                localStorage.id = btoa(data.comumUsers[0].id)
                $cookies.set("user", btoa(data.comumUsers[0].id), 3600*30)
                window.location.href = '/dashboard'
                console.log($cookies.keys())
                this.snack.snackbar = true;
                this.snack.text = "Login realizado com sucesso!"
            } else {
                console.info("Email e/ou senha nao batem!")
                this.snack.snackbar = true;
                this.snack.text = "Senha e/ou email incorreto(s)"
            }
        },
    }
}

</script>