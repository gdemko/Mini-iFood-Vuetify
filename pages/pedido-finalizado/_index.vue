<template>
    <div>
        <b-container class="bv-example-row">
            <b-row class="text-center mb-1">
                <b-col>
                    <b-card block bg-variant="success" text-variant="white" class="text-center" cols="12" md="auto">
                        <b-card-text>{{user.name}} seu pedido foi registrado com Sucesso!! Tempo médio para retirada, 15 a 30 minutos. </b-card-text>
                    </b-card>
                </b-col>
            </b-row>
            <b-row class="text-center mb-1">
                <b-col>
                    <b-card block bg-variant="danger" text-variant="white" class="text-center">
                        <b-card-text>Número do Pedido: {{this.$route.params.index}}</b-card-text>
                    </b-card>
                </b-col>
            </b-row>
            <b-row class="text-center mb-1">
                <b-col>
                    <b-card block bg-variant="info" text-variant="white" class="text-center">
                        <b-card-text>Agradecemos pela sua preferência, bom apetite e não esqueça de nos mencionar nas redes sociais. ^-^</b-card-text>
                    </b-card>
                </b-col>
            </b-row>
        </b-container>
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
