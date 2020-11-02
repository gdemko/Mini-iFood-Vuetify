<template>
  <v-card>
    <v-row>
      <v-col cols="7" class="font-weight-bold">
        Produto
      </v-col>
      <v-col cols="5" class="font-weight-bold">
        Quantidade
      </v-col>
    </v-row>
    <slot></slot>
    <slot name="footer"></slot>
  </v-card>
</template>

<script>
export default {

}
</script>
