<template>
  <v-app id="inspire">
    <v-toolbar color="indigo" dark fixed app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title>Приложение учета пользователей</v-toolbar-title>
      <v-spacer></v-spacer>
      <div class="hidden-sm-and-down">
        <v-btn flat>About</v-btn>
        <v-btn flat>Contact</v-btn>
        <router-link to="/login">
          <v-btn flat>Login</v-btn>
        </router-link>
      </div>
    </v-toolbar>
    <v-content>

    </v-content>
    <v-footer color="indigo justify-center" app>
      <span class="white--text">&copy; 2018 - Инсистем</span>
    </v-footer>

  </v-app>
</template>

<script>

export default {
  name: 'AppMainForm',
  data: () => ({
    drawer: null
  }),
  props: {
    source: String
  }
}
</script>

<style scoped>

</style>
