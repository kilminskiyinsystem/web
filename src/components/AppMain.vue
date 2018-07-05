<template xmlns:>
  <v-app>
    <div v-show="show">
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
                      v-model="loginForm"
                      prepend-icon="person"
                      name="loginForm"
                      label="Логин"
                      type="text"
                      required
                    ></v-text-field>
                    <v-text-field
                      v-model="passwordForm"
                      id="password"
                      prepend-icon="lock"
                      name="passwordForm"
                      label="Пароль"
                      type="password"
                      required
                    ></v-text-field>
                  </v-form>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="primary" @click.native="Submit()">Login</v-btn>

                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-content>

    </div>

    <div v-show="!show">

      <v-toolbar color="indigo" dark fixed app>
        <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
        <v-toolbar-title>Приложение учета пользователей</v-toolbar-title>
        <v-spacer></v-spacer>
        <div class="hidden-sm-and-down">
          <v-btn flat>{{fio}}</v-btn>
          <v-btn flat>{{loginForm}}</v-btn>
          <v-btn flat @click.native="Login()">Выход</v-btn>
        </div>

        <v-tabs
          slot="extension"
          v-model="model"
          centered
          color="cyan"
          slider-color="yellow"
        >

          <v-tab
            :key="'view'"
          >
            Просмотр
          </v-tab>
          <v-tab
            :key="'admin'"
          >
            Администрирование
          </v-tab>
        </v-tabs>
      </v-toolbar>

      <v-content>

        <v-tabs-items v-model="model">
          <v-tab-item
            :id="`view`"
          >
            <v-card flat>

              <h3>Просмотр учетных записей</h3>
              <div v-for="(user, key, index) in users" v-bind:key="index">
                <v-layout row style="max-width: 50%; margin: auto;">

                  <v-text-field
                    label="Логин пользователя"
                    v-model="user.login"
                    outline
                    :aria-readonly="users.login"
                  ></v-text-field>

                  <v-text-field
                    label="Фамилия"
                    v-model="user.vSecondName"
                    :aria-readonly="users.vSecondName"
                    outline
                  ></v-text-field>

                  <v-text-field
                    label="Имя"
                    v-model="user.vFirstName"
                    :aria-readonly="users.vFirstName"
                    outline
                  ></v-text-field>

                  <v-text-field
                    label="Отчество"
                    v-model="user.vPatronymic"
                    :aria-readonly="users.vPatronymic"
                    outline
                  ></v-text-field>

                </v-layout>

              </div>

            </v-card>
          </v-tab-item>

          <v-tab-item
            :id="`admin`"
          >
            <v-card flat>

              <h3>Добавление учетной записи</h3>
              <div style="max-width: 50%; margin: auto;">
                <v-form>
                  <v-container>
                <v-layout column>

                  <v-card-text>
                    <v-form>

                    <v-layout row>
                      <v-text-field
                        v-model="vLogin"
                        prepend-icon="person"
                        name="login"
                        label="Логин"
                        type="text"
                        required
                      ></v-text-field>

                      <v-text-field
                        v-model="vPassword"
                        :append-icon="show1 ? 'visibility_off' : 'visibility'"
                        :rules="[rules.required, rules.min]"
                        :type="show1 ? 'text' : 'password'"
                        name="input-10-1"
                        label="Пароль"
                        hint="Пароль не менее 6 символов"
                        counter
                        @click:append="show1 = !show1"
                      ></v-text-field>

                  </v-layout>
                </v-form>
                </v-card-text>

                  <v-layout row>
                  <v-flex xr3>
                    <v-text-field
                      v-model="vSecondName"
                      :rules="[rules.required, rules.counter]"
                      label="Фамилия"
                      counter
                      maxlength="50"
                      required
                    ></v-text-field>
                  </v-flex>

                  <v-flex>
                    <v-text-field
                      v-model="vFirstName"
                      :rules="[rules.required, rules.counter]"
                      label="Имя"
                      counter
                      maxlength="50"
                      required
                    ></v-text-field>
                  </v-flex>

                  <v-flex>
                    <v-text-field
                      v-model="vPatronymic"
                      :rules="[rules.required, rules.counter]"
                      label="Отчество"
                      counter
                      maxlength="50"
                      required
                    ></v-text-field>
                  </v-flex>
                  </v-layout>

                  <v-layout row>

                    <v-flex xs12 sm6 md4>
                      <v-menu
                        ref="menu"
                        :close-on-content-click="false"
                        v-model="menu"
                        :nudge-right="40"
                        :return-value.sync="vDate"
                        lazy
                        transition="scale-transition"
                        offset-y
                        full-width
                        min-width="290px"
                      >
                        <v-text-field
                          slot="activator"
                          v-model="vDate"
                          label="Дата рождения"
                          prepend-icon="event"
                          readonly
                          required
                        ></v-text-field>
                        <v-date-picker v-model="vDate" no-title scrollable>
                          <v-spacer></v-spacer>
                          <v-btn flat color="primary" @click="menu = false">Cancel</v-btn>
                          <v-btn flat color="primary" @click="$refs.menu.save(vDate)">OK</v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-flex>

                  <v-flex>
                    <v-text-field
                      v-model="vPosition"
                      label="Должность"
                      counter
                    ></v-text-field>
                  </v-flex>

                  <v-flex>
                    <v-text-field
                      v-model="vSubdivision"
                      label="Подразделение"
                      counter
                    ></v-text-field>
                  </v-flex>
                  </v-layout>

                  <v-layout row>
                  <v-flex>
                    <v-text-field
                      :mask="mask"
                      v-model="value"
                      :rules="[rules.required]"
                      label="Телефон"
                    ></v-text-field>
                  </v-flex>

                  <v-flex>
                    <v-text-field
                      v-model="vEmail"
                      :rules="[rules.required, rules.email]"
                      label="E-mail"
                    ></v-text-field>
                  </v-flex>
                  </v-layout>

                </v-layout>

                  </v-container>
                </v-form>

                <v-btn color="primary" @click.native="Add()">Добавить</v-btn>

              </div>

              <h3>Изменение, удаление учетных записей</h3>
              <div v-for="(user, key, index) in users" v-bind:key="index">
                <v-layout row style="max-width: 50%; margin: auto;">

                    <v-text-field
                      label="Логин пользователя"
                      v-model="user.login"
                      outline
                    ></v-text-field>

                    <v-text-field
                      label="Пароль"
                      v-model="user.password"
                      outline
                    ></v-text-field>

                  <v-btn color="error" @click.native="Delete(key)">Удалить</v-btn>
                </v-layout>

              </div>

            </v-card>
          </v-tab-item>
        </v-tabs-items>

      </v-content>
      <v-footer color="indigo justify-center" app>
        <span class="white--text">&copy; 2018 - Инсистем</span>
      </v-footer>
    </div>

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
  name: 'AppMain',
  data: function () {
    return {
      loginForm: null,
      passwordForm: null,
      fio: null,

      vLogin: null,
      vPassword: null,
      vSecondName: null,
      vFirstName: null,
      vPatronymic: null,
      vPosition: null,
      vSubdivision: null,
      vEmail: null,
      vDate: null,

      users: [
        { login: 'admin', password: 'admin', vSecondName: 'Петров', vFirstName: 'Петр', vPatronymic: 'Петрович' },
        { login: 'user', password: 'user', vSecondName: 'Сидоров', vFirstName: 'Сидор', vPatronymic: 'Сидорович' }
      ],

      menu: false,
      alert: false,
      show: true,
      model: 'admin',
      mask: 'phone',
      email: '',
      show1: false,
      rules: {
        required: value => !!value || 'Required.',
        counter: value => value.length <= 50 || 'Max 50 characters',
        min: v => v.length >= 6 || 'Вы ввели меньше 6 символов',
        email: value => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
          return pattern.test(value) || 'Invalid e-mail.'
        }
      }
    }
  },
  methods: {
    Submit () {
      let login = false
      for (var item in this.users) {
        if (this.loginForm === this.users[item].login && this.passwordForm === this.users[item].password) {
          login = true
          localStorage.setItem('CurrentUser', `${this.loginForm} ${this.users[item].vSecondName} ${this.users[item].vFirstName} ${this.users[item].vPatronymic}`)
          this.fio = `${this.users[item].vSecondName} ${this.users[item].vFirstName} ${this.users[item].vPatronymic}`
        }
      }
      if (login) {
        this.show = false
        this.alert = false
      } else {
        this.alert = true
      }
    },
    Login () {
      this.show = true
    },
    Add: function () {
      alert(`Добавление пользователя c логином ${this.vLogin} произведено!`)
      this.users[this.users.length] = {
        login: this.vLogin,
        password: this.vPassword,
        vPassword: this.vPassword,
        vSecondName: this.vSecondName,
        vFirstName: this.vFirstName,
        vPatronymic: this.vPatronymic,
        vPosition: this.vPosition,
        vSubdivision: this.vSubdivision,
        vEmail: this.vEmail,
        vDate: this.vDate
      }
    },
    Delete: function (key) {
      alert(`Удаление пользователя c логином ${this.users[key].login} произведено!`)
      this.users.splice([key], 1)
    }
  }
}

</script>

<style scoped>

</style>
