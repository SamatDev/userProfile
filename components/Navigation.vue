<template>
    <v-list dense>
      <v-list-item link>
        <v-list-item-action>
          <v-icon>mdi-home</v-icon>
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>Profile</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item link @click.prevent="logout">
        <v-list-item-action>
          <v-icon>logout</v-icon>
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title></v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
</template>

<script>
export default {
    methods: {
      logout () {
         this.$store.dispatch('auth/logout')
         this.$router.push('/')
         this.$vuetify.theme.dark = false
      }
    }
}
</script>

<style>

</style>