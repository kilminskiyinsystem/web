<template>
  <div id="app">
    <app-main></app-main>
    <!--<app-main-form></app-main-form>-->
    <!--<app-login-form></app-login-form>-->

    <!--<app-toolbar></app-toolbar>-->
        <!--<router-view/>-->
    <!--<app-login-form></app-login-form>-->
    <!--<app-footer></app-footer>-->
  </div>
</template>

<script>

import AppFooter from './components/AppFooter'
import AppToolbar from './components/AppToolbar'
import AppLoginForm from './components/AppLoginForm'
import AppMainForm from './components/AppMainForm'
import AppMain from './components/AppMain'

export default {
  name: 'App',
  components: {AppFooter, AppToolbar, AppLoginForm, AppMainForm, AppMain}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
