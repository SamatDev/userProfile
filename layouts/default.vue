<template>
  <v-app id="inspire">
    
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
    >
      <nav-app />
    </v-navigation-drawer>
    
    <v-app-bar
      app
      clipped-left
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>User profile App</v-toolbar-title>
      <span style="margin-left: 2rem">Scheme</span>
      <v-switch
        v-model="$vuetify.theme.dark"
        primary
        label="Dark"
        class="random"
      ></v-switch>
    </v-app-bar>

    <v-main>
      <v-container
        class="fill-height"
        fluid
      >
        <nuxt />
      </v-container>
    </v-main>

    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import navApp from '@/components/Navigation'

export default {
  props: {
    source: String,
  },
  components: {
    navApp
  },
  data: () => ({
    drawer: null,
  }),
  created () {
    this.$vuetify.theme.dark = true
  },
  middleware: ['auth']
}
</script>



<style lang="scss">

.container.fill-height{
  justify-content: center;
}
.random{ 
  .v-input__control{
    flex-wrap: nowrap;
    align-items: center;
    justify-content: center;
    margin-left: 1rem;
  }
  .v-input__slot{
    margin-bottom: 0;
  }  
}
</style>
