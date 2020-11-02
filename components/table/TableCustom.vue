<template>
  <div>
    <div class="text-center" v-if="loading">
      <b-spinner style="width: 3rem; height: 3rem;" label="Loading..."></b-spinner>
    </div>
    <div v-else>
      <v-card>
        <v-row class="mb-4">
          <v-col align-self="start">
            <slot name="header"></slot>
            <span class="h2">{{title}}</span>
          </v-col>
        </v-row>
        <v-simple-table
          :items="items"
          :fields="fields"
          responsive="sm"
        >
          <thead >
            <tr >
              <th v-for="(field, index) in fields" :key="index" >{{field.label}}</th>
              <th v-if="!removeOption" class="text-center" >Opções</th>
            </tr>
          </thead>
          <tbody>
            <tr v-if="items.length == 0" >
              <th class="text-center" :colspan="fields.length+1">Nenhum resultado encontrado</th>
            </tr>
            <tr v-else v-for="(item, index) in items" :key="index" >
              <th v-for="(it, index) in item" :key="index" >
                {{it}}
              </th>
              <th v-if="customAction" class="text-center">
                <slot v-bind:index="index" name="action"></slot>
              </th>
              <th class="text-center" v-else>
                <b-button-group>
                  <v-btn v-if="show" :to="route +`/`+item.codigo" >Visualizar</v-btn>
                  <v-btn v-if="edit" :to="route +`/edit/`+item.codigo" variant="primary">Editar</v-btn>
                  <v-btn v-if="remove" @click="destroy(item.codigo)" variant="danger">Excluir</v-btn>
                </b-button-group>
              </th>
            </tr>
          </tbody>
        </v-simple-table>
        <v-btn v-if="buttomAdd" :to="routeAdd" variant="success">Adicionar</v-btn>
        <v-row v-else>
          <v-col cols="12">
            <slot name="footer"></slot>
          </v-col>
        </v-row>
      </v-card>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'

  export default {
    data() {
      return {
        loading: true
      }
    },
    mounted() {
      this.loader()
    },
    props:{
      fields:{
        type: Array,
        required: true
      },
      items:{
        type: Array,
        required: true
      },
      title: {
        type: String,
        required: true
      },
      route:{
        type: String,
      },
      routeAdd: {
        type: String,
      },
      customAction:{
        type: Boolean,
        default: false
      },
      show: {
        type:Boolean,
        default: false
      },
      edit: {
        type:Boolean,
        default: false
      },
      remove: {
        type:Boolean,
        default: false
      },
      buttomAdd: {
        type:Boolean,
        default: false
      },
      removeOption: {
        type:Boolean,
        default: false
      }
    },
    methods:{
      loader(){
        this.loading = false
      },
      destroy(id) {
        Swal.fire({
          title: 'Deseja deletar?',
          text: "Se você deletar não tera como recuperar!",
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#3085d6',
          cancelButtonColor: '#d33',
          confirmButtonText: 'Sim, deletar!',
          cancelButtonText: 'Cancelar'
        }).then((result) => {
          if (result.isConfirmed) {
            this.$axios
            .$delete(
              this.route + `/` + id
            )
            .then(({success, data, message, error_message}) => {
              if(success == true)
              {
                Swal.fire(
                  'Deletado!',
                  message,
                  'success'
                ).then(() => {
                  document.location.reload(true);
                })
              } else {
                this.message = message
                this.error_message = error_message
              }
            })
          }
        })
      }
    }
  }
</script>
