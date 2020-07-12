<template>
  <v-app id="inspire">
    <v-main>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <v-card class="elevation-12">
              <v-toolbar
                color="primary"
                dark
                flat
              >
                <v-toolbar-title>Войти в профиль</v-toolbar-title>
                <v-spacer />
              </v-toolbar>
              <ValidationObserver ref="observer" v-slot="{ validate, reset }">
                <form class="login-form">
                  <ValidationProvider v-slot="{ errors }" name="name" rules="required|max:10">
                    <v-text-field
                      v-model="name"
                      :counter="10"
                      :error-messages="errors"
                      label="Name"
                      required
                    />
                  </ValidationProvider>
                  <ValidationProvider v-slot="{ errors }" name="password" rules="required">
                    <v-text-field
                      v-model="password"
                      :error-messages="errors"
                      label="Password"
                      :type="show4 ? 'text' : 'password'"
                      required
                    />
                  </ValidationProvider>
                  <v-btn class="mr-4" @click="submit">
                    submit
                  </v-btn>
                  <v-btn @click="clear">
                    clear
                  </v-btn>
                </form>
              </ValidationObserver>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { required, max } from 'vee-validate/dist/rules'
import { extend, ValidationObserver, ValidationProvider, setInteractionMode } from 'vee-validate'

setInteractionMode('eager')

extend('required', {
  ...required,
  message: '{_field_} can not be empty'
})

extend('max', {
  ...max,
  message: '{_field_} may not be greater than {length} characters'
})

export default {
  layout: 'signup',
  components: {
    ValidationProvider,
    ValidationObserver
  },
  props: {
    source: String
  },
  data: () => ({
    name: '',
    password: '',
    show4: false
  }),

  methods: {
    submit () {
      this.$refs.observer.validate(this.password, 'required').then(
        async result => {
          if(result) {
            try{
              const formData = {
                login: this.name,
                password: this.password
              }
              
              await this.$store.dispatch('auth/login', formData)
              this.$router.push('/user-profile')
            }catch(e){
              console.log(e)
            }
          }
        }
      )
    },
    clear () {
      this.name = ''
      this.password = ''
      this.$refs.observer.reset()
    }
  }
}
</script>

<style lang="scss" scoped>
  .login-form{
    padding: 1rem;
  }
</style>