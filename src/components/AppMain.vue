<template>
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
          <v-btn flat>{{adminLogin}}</v-btn>
          <v-btn flat>{{adminPassword}}</v-btn>
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
              <!--<v-card-text>view</v-card-text>-->
              <ul>
                <li v-for="user in users" :key="user.login">
                  <!--<input v-model="user.login">-->
                  {{user.login}} {{user.password}}
                </li>
              </ul>
            </v-card>
          </v-tab-item>
          <v-tab-item
            :id="`admin`"
          >
            <v-card flat>
              <v-card-text>Добавление, удаление, изменение учетных записей</v-card-text>
              <div v-for="(user, key, index) in users" v-bind:key="index">
                {{ key + 1}}:
                <input v-model="user.login">
                <input v-model="user.password">
                <v-btn color="error" @click.native="Delete(key)">Удалить</v-btn>
              </div>

              <div>

                <v-layout column wrap>

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vSecondName"-->
                      <!--:vrules="[rules.required, rules.counter]"-->
                      <!--label="Фамилия"-->
                      <!--counter-->
                      <!--maxlength="50"-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vFirstName"-->
                      <!--:vrules="[rules.required, rules.counter]"-->
                      <!--label="Имя"-->
                      <!--counter-->
                      <!--maxlength="50"-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vPatronymic"-->
                      <!--:vrules="[rules.required, rules.counter]"-->
                      <!--label="Отчество"-->
                      <!--counter-->
                      <!--maxlength="50"-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vPosition"-->
                      <!--:vrules="[rules.required, rules.counter]"-->
                      <!--label="Должность"-->
                      <!--counter-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vSubdivision"-->
                      <!--:vrules="[rules.required, rules.counter]"-->
                      <!--label="Подразделение"-->
                      <!--counter-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-card>-->
                    <!--<v-card-text>-->
                      <!--<v-text-field :mask="mask" v-model="value" label="Value"></v-text-field>-->
                    <!--</v-card-text>-->
                  <!--</v-card>-->

                  <!--<v-flex xs12 sm6>-->
                    <!--<v-text-field-->
                      <!--v-model="vEmail"-->
                      <!--:erules="[rules.required, rules.email]"-->
                      <!--label="E-mail"-->
                    <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                  <!--<v-flex xs12 sm6>-->
                  <!--<v-text-field-->
                  <!--v-model="vPassword"-->
                  <!--:append-icon="show1 ? 'visibility_off' : 'visibility'"-->
                  <!--:prules="[rules.required, rules.min]"-->
                  <!--:type="show1 ? 'text' : 'password'"-->
                  <!--name="input-10-1"-->
                  <!--label="Normal with hint text"-->
                  <!--hint="At least 6 characters"-->
                  <!--counter-->
                  <!--@click:append="show1 = !show1"-->
                  <!--&gt;</v-text-field>-->
                  <!--</v-flex>-->

                </v-layout>
                <!--+1. Фамилия * (длина 50)-->
                <!--+2. Имя * (длина 50)-->
                <!--+3. Отчество * (длина 50)-->
                <!--4. Дата рождения *-->
                <!--+5. Должность-->
                <!--+6. Подразделение-->
                <!--+7. Телефон * (сотовый)-->
                <!--+8. EMail-->
                <!--+9. Пароль (пароль не менее 6 символов) *-->
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
      vSecondName: null,
      vFirstName: null,
      vPatronymic: null,
      vPosition: null,
      vSubdivision: null,
      vPassword: null,
      vEmail: null,
      vDate: null,
      password: null,
      alert: false,
      show: true,
      adminLogin: 'xxx',
      adminPassword: 'xxx',
      model: 'admin',
      users: [
        {login: 'xxx', password: 'xxx'},
        {login: 'UserLogin', password: '12345678'}
      ],
      mask: 'phone',
      title: 'Preliminary report',
      email: '',
      show1: false

    }
  },
  methods: {
    Submit () {
      console.log(`Email is ${this.login} and Password is ${this.password}`)
      const result = true
      this.adminLogin = 'xxx'
      this.adminPassword = 'xxx'
      // this.login === this.adminLogin && this.password === this.adminPassword
      if (result) {
        this.show = false
        this.alert = false
      } else {
        this.alert = true
      }
    },
    Login () {
      this.show = true
    },
    Delete: function (key) {
      debugger
      alert(`Удаление пользователя c логином ${this.users[key].login} и паролем ${this.users[key].password} произведено!`)
      this.users.splice([key], 1)
    }
  }
}

</script>

<style scoped>

</style>
