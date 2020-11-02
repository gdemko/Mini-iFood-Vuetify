<template>
  <div>
    <h1>{{title}}</h1>
    <v-card>
      <slot></slot>
      <template v-slot:footer>
        <v-btn v-if="footer" variant="success" type="submit">Salvar</v-btn>
        <v-btn v-if="footer" @click="clear()" variant="primary">Limpar</v-btn>
        <v-btn :to="routeBack">Voltar</v-btn>
      </template>
    </v-card>
  </div>
</template>

<script>
export default {
  props:{
    title: {
      type: String,
      required: true
    },
    routeBack: {
      type: String
    },
    footer: {
      default: false,
      type: Boolean
    }
  },
  methods:{
    clear(){
      this.$emit("clear", true)
    }
  }
}
</script>
