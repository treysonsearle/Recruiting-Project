<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-app-bar-title>iScout Recruiting</v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn href="https://github.com/HazardScout/iScout-Recruiting-Project" target="_blank">
        <span class="mr-2">GitHub</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <Main />

  </v-app>
</template>

<script>
import Main from './components/Main';

export default {
  components: {
    Main,
  },
};
</script>
