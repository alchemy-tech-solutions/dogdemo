<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>My Super</span>
        <span class="font-weight-light">DOG APP</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">v1.0</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <DogApp/>
    </v-content>
  </v-app>
</template>

<script>
import DogApp from "./components/DogApp";

export default {
  name: 'App',
  components: {
      DogApp,
  },
  data () {
    return {
      //
    }
  }
}
</script>
