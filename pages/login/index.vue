<template>
  <div class="container">
    <div>
      <VuetifyLogo />
       <v-form @submit.prevent="onSubmit">
          <v-text-field
            id="input-1"
            v-model="form.email"
            label="E-mail"
            :rules="rules"
            type="email"
            required
            :state="validation"
          ></v-text-field>

          <v-text-field
            id="input-2"
            v-model="form.password"
            label="Senha"
            type="password"
            required
            :state="validation"
          ></v-text-field>

          <v-btn
            color="secondary"
            depressed
            elevation="4"
            type="submit"
          >Login</v-btn>
       </v-form>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'login',
  data() {
      return {
        form: {
          email: '',
          password: '',
        },
        show:true,
        validation:null,
        rules: [
        value => !!value || 'Required.',
        value => (value && value.length >= 3) || 'Min 3 characters',
      ],
      }
    },
    methods: {
      onSubmit(e) {
        e.preventDefault()
         this.$auth
        .loginWith("local", {
          data: {
            email: this.form.email,
            password: this.form.password
          }
        })
        .then((response) => {
          this.validation = true
          console.log('entrei')
          document.location.reload(true);
        }).catch(({response: {
          data: { error },
          status
        }}) => {
          if(status == 400)
          {
            this.validation = false
          }
        })
      },
    }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
