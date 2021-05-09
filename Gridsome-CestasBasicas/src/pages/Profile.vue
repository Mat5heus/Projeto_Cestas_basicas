<template>
    <Layout>
        <v-container class="mb-15 mt-10">
            <v-row justify="space-around">
                <v-col
                    cols="2"
                    sm="2"
                >
                    <v-avatar
                        color="primary"
                        size="128"
                        
                    >
                        <v-img
                            v-if="user.image != null"
                            id="userPicture"
                            :src="user.image"
                            :alt="user.name"
                        ></v-img>
                        <v-icon 
                            v-else
                            dark
                        >
                        mdi-account-circle
                        </v-icon>
                    </v-avatar>
                       
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12" class="text-center text-h6 font-weight-bold">
                    {{ user.name }}
                </v-col>
            </v-row>
            <v-row >
                <v-col cols="12" sm="6">
                    <v-text-field
                        v-model="user.email"
                        :value="user.email"
                        label="Email"
                        solo
                    ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                    <v-text-field
                        v-model="user.name"
                        :value="user.name"
                        label="Nome"
                        solo
                    ></v-text-field>
                </v-col>
                
            </v-row>
            <v-row>
                <v-col cols="12" sm="6">
                    <v-text-field
                        v-model="user.nascimento"
                        :value="user.nascimento"
                        label="Nascimento"
                        solo
                    ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                    <v-textarea
                    v-model="user.bio"
                    :value="user.bio"
                    solo
                    name="input-7-4"
                    label="Bio"
                    ></v-textarea> 
                </v-col>
            </v-row>
            <v-row justify="space-around">
                 <v-col cols="2" sm="1">
                     <v-btn
                        dark
                        to="/dashboard"
                     >
                        Voltar
                    </v-btn>
                </v-col>
                <v-col cols="2" sm="1">
                    <v-btn dark>
                        Salvar
                    </v-btn>
                </v-col>
               
            </v-row>
        </v-container>
    </Layout>
</template>
<script>
import { GraphQLClient, gql } from 'graphql-request'
export default {
    data () {
        return  {
            user: {
                name:'',
                email:'',
                image:'',
                bio:'',
                nascimento:''
            }
        }
    },
    async mounted() {
        const endpoint = 'http://localhost:1337/graphql'

        let id = atob($cookies.get('user'))

        const graphQLClient = new GraphQLClient(endpoint)
        const query = gql`{
        comumUser(id:${id}) {
            id
            Name
            email
            bio
            birthday
            image {
                url
            }
        }
        }
        `
        await graphQLClient.request(query).then(data => {
        if(data.comumUser != undefined) {
            console.log(data)
            this.user.image = `http://localhost:1337${data.comumUser.image.url}`
            this.user.name = data.comumUser.Name
            this.user.email = data.comumUser.email
            this.user.bio = data.comumUser.bio;
            this.user.nascimento = data.comumUser.nascimento;
        }
        })
  },
}

</script>
