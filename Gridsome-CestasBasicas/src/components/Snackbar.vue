<template>
   <v-snackbar
      v-model="snack.snackbar"
      :multi-line="snack.multiLine"
      :timeout="timeout"
    >
      {{ snack.text }}

      <template v-slot:action="{ attrs }">
        <v-btn
          color="red"
          text
          v-bind="attrs"
          @click="onSnackClick(false)"
        >
          Fechar
        </v-btn>
      </template>
    </v-snackbar>
</template>
<script>
  export default {
    props: ['snack'],
    data() {
        return {
            timeout: 2000
        }
    },
    methods: {
        onSnackClick(boo) {
            this.$emit('onSnack',boo)
        },
    }
  }
</script>