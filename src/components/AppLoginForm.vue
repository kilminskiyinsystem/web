<template>
  <v-app id="inspire">
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="primary">
                <v-toolbar-title>Авторизация пользователя</v-toolbar-title>
                <v-spacer></v-spacer>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    v-model="login"
                    prepend-icon="person"
                    name="login"
                    label="Логин"
                    type="text"
                    required
                  ></v-text-field>
                  <v-text-field
                    v-model="password"
                    id="password"
                    prepend-icon="lock"
                    name="password"
                    label="Пароль"
                    type="password"
                    required
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <router-link to="router">
                  <v-btn color="primary" @click.native="submit">Login</v-btn>
                </router-link>

              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>

    <div>

      <v-alert
        :value="alert"
        type="error"
        transition="scale-transition"
      >
        Логин или пароль введен неверно. Попробуйте еще раз.
      </v-alert>
    </div>

  </v-app>
</template>

<script>
export default {
  name: 'AppLoginForm',
  data: () => ({
    login: null,
    password: null,
    alert: false,
    router: { path: `/user/` }
  }),
  props: {
    source: String
  },
  methods: {
    submit () {
      console.log(`Email is ${this.login} and Password is ${this.password}`)

      this.alert = true
    }
  }
}
</script>

<style scoped>

</style>
