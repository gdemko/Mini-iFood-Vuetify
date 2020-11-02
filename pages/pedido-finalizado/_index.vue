<template>
    <div>
        <v-container class="bv-example-row">
            <v-row class="text-center mb-1">
                <v-col>
                    <v-card color="success" block text-variant="white" class="text-center" cols="12" md="auto">
                        <v-card-text>{{user.name}} seu pedido foi registrado com Sucesso!! Tempo médio para retirada, 15 a 30 minutos. </v-card-text>
                    </v-card>
                </v-col>
            </v-row>
            <v-row class="text-center mb-1">
                <v-col>
                    <v-card block color="red" text-variant="white" class="text-center">
                        <v-card-text>Número do Pedido: {{this.$route.params.index}}</v-card-text>
                    </v-card>
                </v-col>
            </v-row>
            <v-row class="text-center mb-1">
                <v-col>
                    <v-card block color="info" text-variant="white" class="text-center">
                        <v-card-text>Agradecemos pela sua preferência, bom apetite e não esqueça de nos mencionar nas redes sociais. ^-^</v-card-text>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
export default {
    data() {
    return {
      user: this.$auth.user
    }
  },
}
</script>
