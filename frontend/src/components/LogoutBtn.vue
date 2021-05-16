<template>
    <v-dialog
        transition="dialog-bottom-transition"
        width="400"
    >
        <template
         v-slot:activator="{ on, attrs }"
         
        >
        <v-btn
            v-model="user"
            v-if="user"
            dark
            v-bind="attrs"
            v-on="on"
            class="mr-2 ml-1"
        >
            Sair
        </v-btn>
        <v-btn
            v-model="user"
            v-if="user"
            dark
            class="mr-2 ml-1"
            to="/dashboard"
        >
            <v-icon>
                mdi-view-dashboard
            </v-icon>
        </v-btn>
        </template>
        <template v-slot:default="dialog">
        <v-card 
            color="rgb(255, 198, 92)"
        >
            <v-toolbar
            dark
            >
                Haaah.. Você já vai?
            </v-toolbar>
            <v-card-text>
            <div class="pa-10">
                <v-container>
                    <v-row class="justify-center">
                        <v-col cols="12" sm="6">
                            <v-btn
                                width="100"
                                height="50"
                                class="font-weight-bold text-h6 text-center"
                                @click="logout()"
                            >
                                SIM
                            </v-btn>
                        </v-col>
                        <v-col cols="12" sm="6">
                           <v-btn
                                width="100"
                                height="50"
                                class="font-weight-bold text-h6"
                                @click="dialog.value = false"
                           >
                               NÃo
                           </v-btn>
                        </v-col>
                    </v-row>
                </v-container>
            </div>
            </v-card-text>
        </v-card>
        </template>
    </v-dialog>
</template>
<script>
export default {
    data () {
        return {
            user: $cookies.isKey("user"),
            dialog: {
                value: false
            },
        }
    },
    mounted() {
    },
    methods: {
        logout() {
            $cookies.remove("user")  
            localStorage.id = null
            window.location.href = '/'
        },
    }
}

</script>